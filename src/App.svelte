<script lang="ts">
	import Timer from "./components/Timer.svelte";
	import Popup from "./components/Popup.svelte";

	let rounds = 3;

</script>

<main>
	<Timer duration={30 * 60} />
</main>

<style>
	main {
		height: 100vh;
		width: 100%;

		display: grid;
		place-items: center;
	}
</style>
