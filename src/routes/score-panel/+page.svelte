<script lang="ts">
	import ScoreController from '$lib/components/score/ScoreController.svelte';
	import ScorePanel from '$lib/components/score/ScorePanel.svelte';
	import TeamScore from '$lib/components/score/TeamScore.svelte';

	interface Score {
		home: {
			team: string;
			score: string;
			color: string;
			img_url: string;
			reversed: boolean;
		};
		away: {
			team: string;
			score: string;
			color: string;
			img_url: string;
			reversed: boolean;
		};
	}
	let stateDefault: Score = {
		home: {
			team: 'psg',
			score: '0',
			color: '#3b82f6',
			img_url:
				'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQqoMKAbWvTpH2aSe9zjm5q65M6cYtSpgfY6A&s',
			reversed: false
		},
		away: {
			team: 'Liverpool',
			score: '1',
			color: '#dc2626',
			img_url: 'https://static.wikia.nocookie.net/liverpoolfc/images/b/b2/Liverbird.png',
			reversed: true
		}
	};
	let home_team: string = $state(stateDefault.home.team);
	let home_score: string = $state(stateDefault.home.score);

	let away_team: string = $state(stateDefault.away.team);
	let away_score: string = $state(stateDefault.away.score);
</script>

{#snippet team_home()}
	<TeamScore
		team={home_team}
		score={home_score}
		color={stateDefault.home.color}
		img_url={stateDefault.home.img_url}
	/>
{/snippet}

{#snippet team_away()}
	<TeamScore
		team={away_team}
		score={away_score}
		color={stateDefault.away.color}
		img_url={stateDefault.away.img_url}
		reversed={stateDefault.away.reversed}
	/>
{/snippet}

<div class="m-6">
	<ScorePanel {team_home} {team_away} />
	<ScoreController
		bind:team_home={home_team}
		bind:score_home={home_score}
		bind:team_away={away_team}
		bind:score_away={away_score}
	/>
</div>
