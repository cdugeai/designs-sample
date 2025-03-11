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

<div class="flex items-center gap-1" class:flex-row-reverse={reversed}>
	<img class:show={displayImages} src={img_url} alt="" class="hide h-8" />
	<p
		class={'team  px-2 font-semibold text-nowrap text-white uppercase ' + className}
		style={'background-color: ' + backgroundColor}
	>
		{team}
	</p>
	<p class="score text-8xl font-bold">{score}</p>
</div>

<style>
	.team {
		font-size: 24px;
	}

	.score {
		font-size: 24px;
	}

	.hide {
		display: none;
	}

	.show {
		display: inline-block;
	}
</style>
