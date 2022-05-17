<script lang="ts">
	import Timer from "./components/Timer.svelte";
	import Popup from "./components/Popup.svelte";
	import Settings from "./components/Settings.svelte";

	enum PAGE {
		FOCUS,
		SETTINGS,
	}

	let page = PAGE.FOCUS;

	let rounds = 3;
	let duration = 25;
</script>

<svelte:head>
	<link
		rel="stylesheet"
		href="https://unpkg.com/mono-icons@1.0.5/iconfont/icons.css"
	/>
</svelte:head>

<main>
	{#if page === PAGE.FOCUS}
		<Timer {duration} autostart={false}/>
		<div>
			<i class="mi mi-settings" on:click={() => page = PAGE.SETTINGS} />
		</div>
	{:else}
		<Settings bind:duration={duration}/>
		<div>
			<i class="mi mi-arrow-left" on:click={() => page = PAGE.FOCUS} />
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
