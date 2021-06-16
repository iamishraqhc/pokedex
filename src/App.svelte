<script>
  import { onMount } from 'svelte'
  import ky from 'ky'

  let pokemons = []

  onMount(async () => {
    let url = 'https://pokeapi.co/api/v2/pokemon'
    const data = await ky.get(url).json()

    pokemons = data.results
  })
</script>

<div class="container mt-8">
  <ul class="grid sm:grid-cols-2 md:grid-cols-3 sm:col-gap-6 row-gap-4">
    {#each  pokemons as { name, url }, index (index)}
      <li>
        <article class="flex flex-xol items-center max-w-sm rounded overflow-hidden shadow-lg">
          <div class="px-6 py-4">
            <h2 class="font-bold text-xl mb-2">{name}</h2>
          </div>
          <img class="w-24 h-24" src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/{index + 1}.png" alt="" />
        </article>
      </li>      
    {/each}
  </ul>
</div>


