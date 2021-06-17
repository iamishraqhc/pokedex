<script>
    export let name
    export let url

    const urlArray = url.split('/')
    const indexLocation = urlArray.length - 2

    const index = urlArray[indexLocation]
    const imageUrl = `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${index}.png`
</script>

