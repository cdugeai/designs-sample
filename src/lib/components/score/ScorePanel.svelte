<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		team_home: Snippet;
		team_away: Snippet;
	}

	let { team_home, team_away }: Props = $props();
</script>

<div class="flex">
	{@render team_home()}
	<p class="mx-2 text-4xl font-extrabold">-</p>
	{@render team_away()}
</div>
