<script lang="ts">
	interface Props {
		team: string;
		score: string;
		color: string;
		img_url: string;
		class?: string;
		reversed?: boolean;
	}
	let {
		team,
		score,
		reversed,
		class: className,
		img_url,
		color: backgroundColor
	}: Props = $props();

	const displayImages: boolean = false;
</script>

<div class:flex-row-reverse={reversed} class=" flex items-center gap-1">
	<img class:show={displayImages} src={img_url} alt="" class="hide h-8" />
	<div
		class={'team px-2 font-semibold text-nowrap text-white uppercase ' + className}
		style={'background-color: ' + backgroundColor}
	>
		{team}
	</div>
	<div class="score text-8xl font-bold">{score}</div>
</div>

<style>
	.team {
		font-size: 24px;
		max-width: 10rem;
		overflow: scroll;
	}

	.score {
		font-size: 24px;
		max-width: 3rem;
		overflow-y: hidden;
		overflow-x: scroll;
	}

	.hide {
		display: none;
	}

	.show {
		display: inline-block;
	}
</style>
