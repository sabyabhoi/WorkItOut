<script lang="ts">
	enum STATE {
		NEW,
		RUNNING,
		PAUSED,
	};
	let state: STATE = STATE.NEW;

	export let duration = 25 * 60;
	let interval: number;

	$: seconds = (duration % 60).toString().padStart(2, 0);
	$: minutes = Math.floor(duration / 60)
		.toString()
		.padStart(2, 0);
	$: formatted = `${minutes}:${seconds}`;

	const start = () => {
		state = STATE.RUNNING;
		interval = setInterval(() => {
			if (state === STATE.RUNNING) {
				duration -= 1;
				if (duration < 0) {
					duration = 100;
					clearInterval(interval);
				}
			}
		}, 1000);
	};

	const pause = () => {
		state = STATE.PAUSED;
	};

	const resume = () => {
		state = STATE.RUNNING;
	};

	const reset = () => {
		state = STATE.NEW;
		clearInterval(interval);
	};
</script>

<div>
	<div class="display">
		<h1>{formatted}</h1>
	</div>
	<div class="buttons">
		{#if state === STATE.NEW}
			<button on:click={start}> start </button>
		{/if}
		{#if state === STATE.RUNNING}
			<button on:click={pause}> pause </button>
		{/if}
		{#if state === STATE.PAUSED}
			<button on:click={resume}> resume </button>
		{/if}
		{#if state === STATE.PAUSED || state === STATE.RUNNING}
			<button on:click={reset}> reset </button>
		{/if}
	</div>
</div>

<style>
	div {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	h1 {
		font-size: 10rem;
	}

	.buttons {
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		column-gap: 1rem;
	}
	.display {
		display: flex;
		flex-direction: row;
	}
</style>
