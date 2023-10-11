<script lang="ts">
  import svelteLogo from './assets/svelte.svg'
  import viteLogo from '/vite.svg'
  import Counter from './lib/Counter.svelte'

  let lambdaValue = "Fetching data..."; // Default value

  async function fetchLambdaValue() {
    try {
      const response = await fetch("https://yft52ipf6ewpjwbvwz35rv57sm0stipx.lambda-url.eu-west-2.on.aws/");
      if (response.ok) {
        const data = await response.json();
        lambdaValue = data.body;
      } else {
        lambdaValue = "Error fetching data 1.";
      }
    } catch (error) {
      console.error(error)
      lambdaValue = "Error fetching data 2.";
    }
  }

  fetchLambdaValue();
</script>

<main>
  <div>
    <a href="https://vitejs.dev" target="_blank" rel="noreferrer">
      <img src={viteLogo} class="logo" alt="Vite Logo" />
    </a>
    <a href="https://svelte.dev" target="_blank" rel="noreferrer">
      <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
    </a>
  </div>
  <h1>Vite + Svelte</h1>

  <div class="card">
    <Counter />
  </div>

  <p>
    Check out <a href="https://github.com/sveltejs/kit#readme" target="_blank" rel="noreferrer">SvelteKit</a>, the official Svelte app framework powered by Vite!
  </p>

  <p class="read-the-docs">
    Click on the Vite and Svelte logos to learn more
  </p>
  <h1>Value from Lambda:</h1>
  <p>{lambdaValue}</p>
</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
</style>
