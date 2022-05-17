<script lang="ts">
	import Timer from "./components/Timer.svelte";
	import Settings from "./components/Settings.svelte";

	enum PAGE {
		FOCUS,
		TIMEOUT,
		SETTINGS,
	}

	let page = PAGE.FOCUS;

	let totalRounds = 3;
	let currentRound = 1;
	let duration = 25;
	let breakDuration = 5;
	let autostart = false;
	let startTimer;

	const nextRound = () => {
		if (currentRound >= totalRounds) {
			currentRound = 1;
			autostart = false;
		} else {
			autostart = true;
			if (page === PAGE.FOCUS) {
				page = PAGE.TIMEOUT;
			} else if (page === PAGE.TIMEOUT) {
				currentRound++;
				page = PAGE.FOCUS;
			}
		}
	};
</script>

<svelte:head>
	<link
		rel="stylesheet"
		href="https://unpkg.com/mono-icons@1.0.5/iconfont/icons.css"
	/>
</svelte:head>

<main>
	{#if page === PAGE.FOCUS}
		<h1>
			ROUND {currentRound}
		</h1>
		<Timer {duration} {autostart} on:end={nextRound} />
		<div>
			<i class="mi mi-settings" on:click={() => (page = PAGE.SETTINGS)} />
		</div>
	{:else if page === PAGE.TIMEOUT}
		<h1>
			BREAK {currentRound}
		</h1>
		<Timer duration={breakDuration} {autostart} on:end={nextRound} />
		<div>
			<i class="mi mi-settings" on:click={() => (page = PAGE.SETTINGS)} />
		</div>
	{:else}
		<Settings bind:duration bind:breakDuration />
		<div>
			<i class="mi mi-arrow-left" on:click={() => (page = PAGE.FOCUS)} />
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

	h1 {
		position: absolute;
		top: 6rem;
	}
</style>
