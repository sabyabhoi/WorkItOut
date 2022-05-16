<script lang="ts">
	import Timer from "./components/Timer.svelte";
	import Popup from "./components/Popup.svelte";
	import Settings from "./components/Settings.svelte";

	enum PAGE {
		TIMER,
		SETTINGS,
	}

	let page = PAGE.TIMER;

	let rounds = 3;
	let started = false;
	let timer;
</script>

<svelte:head>
	<link
		rel="stylesheet"
		href="https://unpkg.com/mono-icons@1.0.5/iconfont/icons.css"
	/>
</svelte:head>

<main>
	{#if page === PAGE.TIMER}
		<Timer duration={10 * 60} bind:this={timer} />
		<div>
			<i class="mi mi-settings" on:click={() => page = PAGE.SETTINGS} />
		</div>
	{:else}
		<Settings/>
		<div>
			<i class="mi mi-arrow-left" on:click={() => page = PAGE.TIMER} />
		</div>
	{/if}
</main>

<style>
	main {
		height: 100vh;
		width: 100%;

		display: grid;
		place-items: center;
	}
	div {
		position: absolute;
		top: 1rem;
		left: 1rem;
		font-size: 1.3rem;
	}
</style>
