<script>
  import svelteLogo from './assets/svelte.svg'
  import viteLogo from '/vite.svg'
  import Counter from './lib/Counter.svelte'
  import {onMount} from 'svelte'

  const URL = `https://saurav.tech/NewsAPI/everything/cnn.json`
  let articles = []
  onMount(async function() {
    const res = await fetch(URL);
    const json = await res.json();
    articles = json["articles"]
  })
</script>

<main>
  <img src="https://dailyplanetdc.files.wordpress.com/2018/12/cropped-daily-planet-logo.jpg?w=656&h=146" alt="">
  <p class="about">
    The Daily Planet is where heros are born and the story continues.
  </p>
  <div class="container">
    {#each articles as article}
        <div class="card">
          <img src="{article.urlToImage}" alt="">
          <div class="card-body">
            <h3>{article.title}</h3>
            <p>{article.description}</p>
            <a href="{article.url}" target="_blank">Read story</a>
          </div>
        </div>
    {/each}
  </div>
</main>

<style>
  h1{
    color: purple;
  }
  .container{
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(305px, 1fr));
    gap: 15px;
  }

  .container > .card img {
    max-width: 100%;
  }
</style>
