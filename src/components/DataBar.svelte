<script>
    import { tweened } from 'svelte/motion'

    export let statColor
    export let value

    let amount = tweened(0)
    $: amount.set(value)
</script>

<div class="flex flex-col items-center justify-center text-white bg-{statColor}" style="width: {amount}%;">
    <span class="text-xs">{value}</span>
</div>
