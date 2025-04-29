<script>
	import blackjack from '$lib/images/blackjack.jpg';

	let deck = [];
	let playerHand = [];
	let dealerHand = [];
	let gameOver = false;
	let message = "Welcome to Totally Honest Blackjack™";

	function initDeck() {
		const suits = ["♠", "♥", "♦", "♣"];
		const values = ["A", "2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K"];
		let d = [];

		for (let suit of suits) {
			for (let value of values) {
				d.push({ suit, value });
			}
		}

		// Shuffle
		for (let i = d.length - 1; i > 0; i--) {
			const j = Math.floor(Math.random() * (i + 1));
			[d[i], d[j]] = [d[j], d[i]];
		}

		return d;
	}

	function cardValue(card) {
		if (["K", "Q", "J"].includes(card.value)) return 10;
		if (card.value === "A") return 11;
		return parseInt(card.value);
	}

	function handValue(hand) {
		let total = hand.reduce((sum, card) => sum + cardValue(card), 0);
		let aces = hand.filter(c => c.value === "A").length;
		while (total > 21 && aces > 0) {
			total -= 10;
			aces--;
		}
		return total;
	}

	function deal() {
		deck = initDeck();
		playerHand = [deck.pop(), deck.pop()];
		dealerHand = [deck.pop(), deck.pop()];
		gameOver = false;
		message = "Your move: Hit or Stand?";
	}

	function hit() {
		if (gameOver) return;
		playerHand = [...playerHand, deck.pop()];
		const total = handValue(playerHand);
		if (total > 21) {
			message = "Bust! The house always wins.";
			gameOver = true;
		}
	}

	function stand() {
		if (gameOver) return;

		// Dealer cheats: keep drawing until exactly 20 or 21
		while (handValue(dealerHand) < 20) {
			dealerHand = [...dealerHand, deck.pop()];
		}

		// If somehow dealer busts (rare), remove last card
		if (handValue(dealerHand) > 21) {
			dealerHand.pop();
		}

		const playerScore = handValue(playerHand);
		const dealerScore = handValue(dealerHand);

		if (dealerScore > 21 || playerScore > dealerScore) {
			message = "You win? That's... unexpected.";
		} else if (playerScore === dealerScore) {
			message = "Push. Nobody wins. Suspicious.";
		} else {
			message = "Dealer wins. Naturally.";
		}
		gameOver = true;
	}
</script>


<!-- Header -->
<div class="grid bg-black">
    <a href="/" class="text-2xl font-bold p-4 text-center text-white">TOTALLY HONEST CASINO</a>
</div>

<!-- Centered Content (No background image) -->
<div class="min-h-screen flex items-center justify-center bg-cover bg-center p-5" style="background-image: url({blackjack}); bg-amber-100">
    <section class="flex flex-col items-center max-w-lg opacity-85 justify-center gap-6 p-10 bg-white rounded-xl shadow-lg">
        <h2 class="text-2xl font-bold">Totally Honest Blackjack™</h2>
        <p>Try your luck at our totally fair Blackjack table!</p>
        <p>Remember: The house always wins... eventually.</p>

        <div class="text-center">
            <h3 class="font-semibold">Your Hand ({handValue(playerHand)})</h3>
            <p>
                {#each playerHand as card}
                    {card.value}{card.suit}{" "}
                {/each}
            </p>
        </div>

        <div class="text-center">
            <h3 class="font-semibold">Dealer's Hand ({gameOver ? handValue(dealerHand) : "?"})</h3>
            <p>
                {#each dealerHand as card, i}
                    {#if i === 0 || gameOver}
                        {card.value}{card.suit}{" "}
                    {:else}
                        ??
                    {/if}
                {/each}
            </p>
        </div>

        <p class="my-4 italic">{message}</p>

        <div class="flex gap-4">
            <button on:click={deal} class="bg-blue-500 text-white px-6 py-2 rounded-lg shadow hover:bg-blue-600 transition">Deal</button>
            <button on:click={hit} class="bg-yellow-500 text-white px-6 py-2 rounded-lg shadow hover:bg-yellow-600 transition">Hit</button>
            <button on:click={stand} class="bg-red-500 text-white px-6 py-2 rounded-lg shadow hover:bg-red-600 transition">Stand</button>
        </div>
    </section>
</div>

<!-- Footer -->
<footer class="bg-black p-3 text-center">
    <p class="footer_text text-white">&copy;TOTALLY HONEST CASINO</p>
</footer>
