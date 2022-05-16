<script lang="ts">
	import Timer from "./components/Timer.svelte";
	import Popup from "./components/Popup.svelte";

	let rounds = 3;
	let started = false;
	let timer;
</script>

<main>
	<Timer duration={10} bind:this={timer}/>
</main>

<style>
	main {
		height: 100vh;
		width: 100%;

		display: grid;
		place-items: center;
	}
</style>
