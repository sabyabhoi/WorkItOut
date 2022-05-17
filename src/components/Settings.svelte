<script>
	export let duration = 25;
	export let breakDuration = 5;
</script>

<div class="settings">
	<div>
		Focus duration:
		<div class="input">
			<input
				type="number"
				min="20"
				max="50"
				bind:value={duration}
				on:change={(e) => (duration = e.target.value)}
			/>
			<button on:click={() => (duration = 25)}>Defaults</button>
		</div>
	</div>
	<div>
		Short break duration:
		<div class="input">
			<input
				type="number"
				min="4"
				max="8"
				bind:value={breakDuration}
				on:change={(e) => (breakDuration = e.target.value)}
			/>
			<button on:click={() => (breakDuration = 5)}>Defaults</button>
		</div>
	</div>
</div>

<style>
	.settings {
		display: flex;
		flex-direction: column;
		row-gap: 2rem;
		width: 50%;
	}

	.input {
		display: flex;
		flex-direction: row;
		column-gap: 1rem;
	}
</style>
