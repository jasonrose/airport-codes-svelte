<script>
  import { onMount } from 'svelte';
  export let id;
  let data = {};
  let webpSupported = window.webpSupported ? '.webp' : '.jpg';

  async function getPage() {
    const res = await fetch(`/assets/data/${id}.json`);
    const json = await res.json();

    if (res.ok) {
      data = json;
    } else {
      throw new Error(json);
    }
  }
  if (id !== 'about') {
    onMount(getPage);
  }
</script>

<style>
  main > * {
   box-sizing: border-box;
  }
  main {
    background-size: cover;
    height: 100%;
    width: 100%;
  }
  section {
    background: rgba(0, 0, 0, 0.8);
    height: 100%;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .data {
    max-width: 500px;
    padding: 20px;
    animation: fadein 0.4s;
  }
  .data h1 {
    text-transform: uppercase;
  }
  .back-container {
    margin: 25px 0;
  }
  .back {
    border: 1px solid #fff;
    padding: 10px 20px;
    border-radius: 4px;
  }
  .back, .back:visited {
    color: #fff;
  }
  @keyframes fadein {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
</style>

{#if id === 'about'}
<main>
  <section>
    <div class="data">
      <div>
          <p>The orginal is found here <a href="https://airportcod.es/">https://airportcod.es/</a></p>
          <p>Airport Codes (svelte) built by <a href="https://twitter.com/richardiii">Richard Torruellas</a> is an iteration of the original designed and built by <a href="https://twitter.com/lynnandtonic">Lynn Fisher</a> and <a href="https://twitter.com/nickcrohn">Nick Crohn</a></p> <p>This is merely an experiment to play with svelte. All credit goes to <a href="https://twitter.com/lynnandtonic">Lynn Fisher</a> and <a href="https://twitter.com/nickcrohn">Nick Crohn</a> for their hard work on the original project.</p>
    </div>
  </section>
</main>
{:else} {#if data.id}
<main style="background-image: url(/assets/images/card/{data.id}{webpSupported})">
  <section>
    <div class="data">
      <div>
        <h1>{data.id}</h1>
        <h2>{data.name}</h2>
        <h3>
          <span class="city">{data.city}</span>
          <span class="country">{data.country}</span>
        </h3>
        <div>
          <p>
            {data.description}
          </p>
        </div>
      </div>
      <div>photo by <a href="{data.imageCreditLink}">{data.imageCredit}</a></div>
      <div class="back-container"><a href="#" class="back">&#8592; back</a></div>
    </div>
  </section>
</main>
{/if} {/if}
