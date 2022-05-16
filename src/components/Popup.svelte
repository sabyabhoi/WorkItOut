<div>
	<div>
		<p>
			Focus duration: <input type="number" min="10" max="60" /> minutes
		</p>
		<p>
			Short-break duration: <input type="number" min="5" max="10" /> minutes
		</p>
		<p>
			Long-break duration: <input type="number" min="15" max="30" /> minutes
		</p>
	</div>
</div>

<style>
	div {
		background-color: white;
		width: 40rem;
		height: 20rem;
		color: black;

		position: fixed;
		z-index: 1;

		border-radius: 1rem;

		display: grid;
		place-items: center;
	}

	div div {
		display: flex;
		flex-direction: column;
		align-items: flex-start;
		justify-content: space-evenly;
		padding-left: 1rem;
	}
</style>
