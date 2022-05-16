<script>
	export let duration = 25;
</script>

<div class="settings">
	<div>
		Focus duration: 
		<div class="input">
			<input
				type="number"
				min="20"
				max="30"
				bind:value={duration}
				on:change={(e) => (duration = e.target.value)}
			/>
			<button on:click={() => duration = 25}>Defaults</button>
		</div>
	</div>
	<div>
		Short break duration: 
		<div class="input">
			<input type="number" min="4" max="8" />
			<button on:click={() => duration = 25}>Defaults</button>
		</div>
	</div>
</div>

<style>

	.settings {
		display: flex;
		flex-direction: column;
		row-gap: 2rem;
	}

	.input {
		display: flex;
		flex-direction: row;
		column-gap: 1rem;
	}

</style>
