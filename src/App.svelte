<script>
  import ky from 'ky'

  import PokemonCard from './components/PokemonCard.svelte'

  let pokemons = []
  let offset = 0
  let amountToLoad = 24

  $: {
    getPokemon(offset)
  }

  async function getPokemon() {
    let url = `https://pokeapi.co/api/v2/pokemon?offset=${offset}&limit=${amountToLoad}`
    const data = await ky.get(url).json()

    pokemons = [...pokemons, ...data.results]
    console.log(pokemons)
  }

  function handleMoreClick(event) {
    offset += amountToLoad
  }

</script>

<header class="flex items-center justify-between w-full bg-red-600 px-8 py-4">
  <h1 class="text-2xl text-white uppercase">Pokédex</h1>
  <p class="text-white">
    Pokemon Cards brought to you by 
    <a href="https://pokeapi.co/" class="text-white underline">PokéAPI</a>
  </p>
</header>
<div class="container mt-8">
  <ul class="grid sm:grid-cols-2 md:grid-cols-3 sm:col-gap-6 row-gap-4">
    {#each  pokemons as { name, url }, index (index)}
      <PokemonCard {name} {url} />
    {/each}
  </ul>

  {#if pokemons.length > 0}
    <button
      class="border border-red-700 font-bold hover:bg-red-700 hover:text-white
      px-4 py-2 rounded text-red-700"
      type="button"
      id="more-button"
      on:click={handleMoreClick}
    >
    Load More
    </button>
  {/if}
</div>
