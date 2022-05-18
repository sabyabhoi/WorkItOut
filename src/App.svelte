<script lang="ts">
	import Timer from "./components/Timer.svelte";
	import Settings from "./components/Settings.svelte";
	import { sendNotification } from '@tauri-apps/api/notification';

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
	const audio = new Audio('sound.oga');

	const nextRound = () => {
		audio.play();
		if (currentRound >= totalRounds) {
			currentRound = 1;
			autostart = false;
		} else {
			autostart = true;
			if (page === PAGE.FOCUS) {
				sendNotification(`Take a break for ${breakDuration} minutes`);
				page = PAGE.TIMEOUT;
			} else if (page === PAGE.TIMEOUT) {
				sendNotification("Alright, break over");
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

		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		row-gap: 3em;
	}
	div {
		position: absolute;
		top: 1rem;
		left: 1rem;
		font-size: 1.3rem;
	}
</style>
