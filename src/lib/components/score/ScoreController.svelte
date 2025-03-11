<script lang="ts">
	let displayControls: boolean = $state(true);

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
</script>

<button onclick={() => (displayControls = !displayControls)}>
	{displayControls ? 'Hide' : 'Show'} controls
</button>

<div class="flex flex-col items-center" class:hide={!displayControls}>
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
	<div class="score-inputs flex">
		<input
			class={'' + inputClass}
			type="number"
			id="score_home"
			placeholder="Home score"
			bind:value={score_home}
		/>
		<input
			class={'' + inputClass}
			type="number"
			id="score_away"
			placeholder="Away score"
			bind:value={score_away}
		/>
	</div>
</div>

<style>
	.button-incr {
		background-color: rebeccapurple;
	}

	.score-inputs,
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
