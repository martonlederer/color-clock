<script lang="ts">
  import { onMount } from 'svelte'
  import invert from 'invert-color'

  let date = new Date()
  $: hours = ('0' + date.getHours()).slice(-2)
  $: minutes = ('0' + date.getMinutes()).slice(-2)
  $: seconds = ('0' + date.getSeconds()).slice(-2)
  $: textColor = invert(`#${ seconds }${ minutes }${ hours }`, true)

  onMount(() => {
		setInterval(() => {
			date = new Date()
		}, 1000)
	})
</script>

<main style="background-color: #{seconds}{minutes}{hours}">
	<div class="time" style="color: {textColor}">
    <h1>#{hours}{minutes}{seconds}</h1>
    <h2>{hours}:{minutes}:{seconds}</h2>
  </div>
</main>

<style lang="sass">

	main
    position: fixed
    top: 0
    left: 0
    right: 0
    bottom: 0
    transition: all .27s

    .time
      position: absolute
      top: 50%
      left: 50%
      transform: translate(-50%, -50%)

      h1, h2
        text-align: center
        margin: 0

      h1
        font-size: 12em

      h2
        font-size: 8em

</style>