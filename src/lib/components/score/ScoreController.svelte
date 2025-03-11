<script lang="ts">
	let displayControls: boolean = $state(false);

	interface Props {
		team_home: string;
		team_away: string;
		score_home: string;
		score_away: string;
	}

	let {
		team_home = $bindable(),
		team_away = $bindable(),
		score_home = $bindable(),
		score_away = $bindable()
	}: Props = $props();

	const inputClass: string =
		'border-input placeholder:text-muted-foreground focus-visible:ring-ring flex h-9 w-full rounded-md border bg-transparent px-3 py-1 text-sm shadow-sm transition-colors focus-visible:ring-1 focus-visible:outline-none';

	function stringIncrement(number_as_str: string, inc_value: number): string {
		const MIN_VALUE: number = 0;
		let number_as_number: number = parseInt(number_as_str);
		let num_incremented: number = number_as_number + inc_value;
		let num_incremented_bounded: number = Math.max(number_as_number + inc_value, MIN_VALUE);
		return num_incremented_bounded.toString();
	}
	function stringIncrementOne(number_as_str: string): string {
		return stringIncrement(number_as_str, 1);
	}
	function stringDecrementOne(number_as_str: string): string {
		return stringIncrement(number_as_str, -1);
	}
</script>

<button class="underline" onclick={() => (displayControls = !displayControls)}>
	{displayControls ? 'Hide' : 'Show'} controls
</button>

<div class="flex flex-col items-center gap-1" class:hide={!displayControls}>
	<div class="team-inputs flex">
		<input
			class={'' + inputClass}
			type="text"
			id="team_home"
			placeholder="Home team"
			bind:value={team_home}
		/>
		<input
			type="text"
			class={'' + inputClass}
			id="team_away"
			placeholder="Away team"
			bind:value={team_away}
		/>
	</div>
	<div class="score-inputs flex justify-around gap-3">
		<div class="flex items-center outline-1">
			<button
				class="button-incr"
				onclick={() => {
					score_home = stringDecrementOne(score_home);
				}}>-</button
			>
			<button
				class="button-incr"
				onclick={() => {
					score_home = stringIncrementOne(score_home);
				}}>+</button
			>
		</div>
		<div class="flex items-center outline-1">
			<button
				class="button-incr"
				onclick={() => {
					score_away = stringDecrementOne(score_away);
				}}>-</button
			>
			<button
				class="button-incr"
				onclick={() => {
					score_away = stringIncrementOne(score_away);
				}}>+</button
			>
		</div>
	</div>
</div>

<style>
	.button-incr {
		background-color: rgba(102, 51, 153, 0.094);
		width: 20px;
	}

	.score-inputs {
		gap: 3rem;
	}

	.team-inputs {
		gap: 1rem;
	}

	.hide {
		display: none;
	}
	input {
		background-color: rgba(236, 188, 188, 0.267);
		border-radius: 5px;
		max-width: 5rem;
	}
</style>
