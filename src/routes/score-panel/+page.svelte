<script>
	import ScorePanel from '$lib/components/score/ScorePanel.svelte';
	import TeamScore from '$lib/components/score/TeamScore.svelte';
</script>

{#snippet team_home()}
	<TeamScore
		team="psg"
		score="0"
		color="#3b82f6"
		img_url="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQqoMKAbWvTpH2aSe9zjm5q65M6cYtSpgfY6A&s"
	/>
{/snippet}

{#snippet team_away()}
	<TeamScore
		team="Liverpool"
		score="1"
		color="#dc2626"
		img_url="https://static.wikia.nocookie.net/liverpoolfc/images/b/b2/Liverbird.png"
		reversed={true}
	/>
{/snippet}

<div class="m-2">
	<ScorePanel {team_home} {team_away} />
</div>
