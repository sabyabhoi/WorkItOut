<script lang="ts">
	enum STATE {
		NEW,
		RUNNING,
		PAUSED,
	}

	let state: STATE = STATE.NEW;
	let startTime: number = 0;
	let elapsedTime: number = 0;
	let oldElapsedTime: number = 0;
	let interval: number;

	$: seconds = (elapsedTime % 60).toString().padStart(2, 0);
	$: minutes = Math.floor(elapsedTime / 60)
		.toString()
		.padStart(2, 0);
	$: formatted = `${minutes}:${seconds}`;

	const start = () => {
		state = STATE.RUNNING;
		oldElapsedTime = 0;
		startTime = Date.now();
		interval = setInterval(() => {
			if (state === STATE.RUNNING)
				elapsedTime =
					Math.floor((Date.now() - startTime) / 1000) + oldElapsedTime;
		}, 1000);
	};

	const reset = () => {
		state = STATE.NEW;
		elapsedTime = 0;
		clearInterval(interval);
	};

	const pause = () => {
		state = STATE.PAUSED;
		oldElapsedTime = elapsedTime;
	};

	const resume = () => {
		startTime = Date.now();
		state = STATE.RUNNING;
	};
</script>

<div>
	<h1>{formatted}</h1>
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

	button {
		border-width: 2px;
		border-color: white;
		border-radius: 0.5rem;
		border-style: solid;
		padding-inline: 2rem;
		padding-block: 0.8rem;
		background: none;
		color: white;
		font-size: 1.2rem;
		text-transform: uppercase;
	}

	button:hover {
		border-color: grey;
		color: grey;
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
</style>
