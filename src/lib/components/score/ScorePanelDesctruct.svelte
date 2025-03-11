<script lang="ts">
	import type { Snippet } from 'svelte';
	import TeamScore from './TeamScore.svelte';

	interface Props {
		team_home_name: string;
		team_away_name: string;
		team_home_score: string;
		team_away_score: string;
		team_home_color: string;
		team_away_color: string;
		team_home_logo_url: string;
		team_away_logo_url: string;
		team_home_reversed: boolean;
		team_away_reversed: boolean;
	}

	let {
		team_home_name,
		team_away_name,
		team_home_score,
		team_away_score,
		team_home_color,
		team_away_color,
		team_home_logo_url,
		team_away_logo_url,
		team_home_reversed,
		team_away_reversed
	}: Props = $props();
</script>

<div class="flex">
	<TeamScore
		team={team_home_name}
		score={team_home_score}
		color={team_home_color}
		img_url={team_home_logo_url}
		reversed={team_home_reversed}
	/>
	<p class="mx-2 text-4xl font-extrabold">-</p>
	<TeamScore
		team={team_away_name}
		score={team_away_score}
		color={team_away_color}
		img_url={team_away_logo_url}
		reversed={team_away_reversed}
	/>
</div>
