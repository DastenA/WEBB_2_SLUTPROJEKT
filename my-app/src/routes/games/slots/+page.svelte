<script>
    import slots from '$lib/images/slots.jpg';

    const symbols = ["🍒", "🍋", "🍊", "🔔", "💎", "7️⃣", "🌝", "☂", "🍉"];

    const symbols_fair = ["🍒", "🍋", "🍊", "🔔", "💎", "7️⃣", "🌝", "☂", "🍉", "🥞", "🧇", "🍧", "🏴‍☠️", "⚜", "😎"]; 

  
    let reels = ["🍒", "🍒", "🍒","🍒"];
    let reels_fair = ["🍒", "🍒",];
    let message = "Why dont you give it a spin?";
    let win = 0
    let attempt = 0
    let win_fair = 0
    let attempt_fair = 0
  
    function spin() {
      reels = [
        symbols[Math.floor(Math.random() * symbols.length)],
        symbols[Math.floor(Math.random() * symbols.length)],
        symbols[Math.floor(Math.random() * symbols.length)],
        symbols[Math.floor(Math.random() * symbols.length)],
      ];
  
      if (reels[0] === reels[1] && reels[1] === reels[2] && reels[2] === reels[3]) {
        message = "Well that was unexpected.";
        win += 1;
        attempt += 1;

      } else {
        message = "You failed but that was too be expected.";
        attempt += 1;
      }
    }

    function spin_fair() {
      reels_fair = [
        symbols_fair[Math.floor(Math.random() * symbols_fair.length)],
        symbols_fair[Math.floor(Math.random() * symbols_fair.length)],
      ];
  
      if (reels_fair[0] === reels_fair[1]) {
        message = "Well that was unexpected.";
        win += 1;
        attempt += 1;

      } else {
        message = "You failed but that was too be expected.";
        attempt += 1;
      }
    }
</script>

    <div class="grid bg-black">
    <a href="/" class="text-2xl font-bold p-4 text-center text-white">TOTALLY HONEST CASINO</a>
    </div>

<div class="min-h-screen flex items-center justify-center bg-cover bg-center p-5" style="background-image: url({slots});">
  <section class="grid grid-rows-[auto,1fr,auto] gap-6 max-w-4xl opacity-85 p-10 bg-white rounded-xl shadow-lg">
  
    <div class="col-span-full text-center">
      <h2 class="text-2xl font-bold">Totally Honest Slots™</h2>
      <p>Bright lights, spinning reels, and the illusion of hope!</p>
      <p>Our state-of-the-art slot machines are powered by RNGs (Rigged Number Generators),</p>
      <p>ensuring that your dreams of winning stay right where they belong — in your head.</p>
    </div>
  
    <div class="grid sm:grid-cols-1 md:grid-cols-2 gap-6">
      
      <div class="space-y-4 text-center p-2 border-2">
        <div class="text-3xl grid grid-cols-4 gap-4 justify-items-center">
          {#each reels as reel}
            <span>{reel}</span>
          {/each}
        </div>
  
        <button class="bg-red-500 text-white px-6 py-2 rounded-lg shadow hover:bg-red-600 transition" on:click={spin}>
          Spin
        </button>
        <p>Your chances of winning are 0.0013%, Goodluck!</p>

      </div>
  
      <div class="space-y-4 text-center p-2 border-2">
        <div class="text-3xl grid grid-cols-2 gap-4 justify-items-center">
          {#each reels_fair as reel_fair}
            <span>{reel_fair}</span>
          {/each}
        </div>
  
        <button class="bg-red-500 text-white px-6 py-2 rounded-lg shadow hover:bg-red-600 transition" on:click={spin_fair}>
          Spin
        </button>
        <p>Your chances of winning are 14.4433%, Goodluck!</p>

      </div>
    </div>
  
    <div class="col-span-full space-y-2 text-center">
      <p class="text-lg">{message}</p>
      <p class="text-lg">Wins: {win}</p>
      <p class="text-lg">Attempts: {attempt}</p>
      <a href="/games/blackjack" class="bg-green-200 p-2 rounded-lg shadow-lg">Wanna try out our rigged Blackjack?</a>
    </div>
  </section>
  
  

</div>

    <footer class="bg-black p-3 text-center">
        <p class="footer_text text-white">&copy;TOTALLY HONEST CASINO</p>
    </footer>

<style>

</style>