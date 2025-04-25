<script>
    import slots from '$lib/images/slots.jpg';

    const symbols = ["🍒", "🍋", "🍊", "🔔", "💎", "7️⃣", "🌝", "☂", "🍉"];
  
    let reels = ["🍒", "🍒", "🍒","🍒"];
    let message = "Why dont you give it a spin?";
    let win = 0
    let attempt = 0
  
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

      } else {
        message = "You failed but that was too be expected.";
        attempt += 1;
      }
    }
</script>

    <div class="grid bg-black">
    <a href="/" class="text-2xl font-bold p-4 text-center">TOTALLY HONEST SLOTS</a>
    </div>


<div class="min-h-screen flex items-center justify-center bg-cover bg-center" style="background-image: url({slots});">
        <section class="flex flex-col items-center max-w-lg opacity-80 justify-center gap-6 p-10 bg-white rounded-xl shadow-lg">
          <h2 class="text-2xl font-bold">Totally Honest Slots™</h2>
          <p>Bright lights, spinning reels, and the illusion of hope!</p>
          <p>Our state-of-the-art slot machines are powered by RNGs (Rigged Number Generators), ensuring that your dreams of winning stay right where they belong — in your head.</p>
      
          <div class="text-6xl flex gap-6">
            {#each reels as reel}
              <span>{reel}</span>
            {/each}
          </div>
      
          <button 
            class="bg-red-500 text-white px-6 py-2 rounded-lg shadow hover:bg-red-600 transition"
            on:click={spin}>
            Spin
          </button>
      
          <p class="text-lg">{message}</p>
          <p class="text-lg">Wins: {win}</p>
          <p class="text-lg">Attempts: {attempt}</p>
          <p>Your chances of winning are 0.0013%, goodluck!</p>
        </section>
</div>

      <footer class="bg-black p-3 text-center">
        <p class="footer_text">&copy;TOTALLY HONEST CASINO</p>
    </footer>

<style>

</style>