<script lang="ts">
	const title: string = 'Roadbook';

	interface Checkpoint {
		name: string;
		distance_from_start: number;
	}

	const checkpoints: Array<Checkpoint> = [
		{ name: 'Depart', distance_from_start: 0 },
		{ name: 'Prendre N118 au ring', distance_from_start: 4 },
		{
			name: 'Sortie 8 St-Quentin-en-Ynes/Jouy-en-Josas/Toussus-le-Noble/Saclay',
			distance_from_start: 10
		},
		{ name: 'Chateaufort', distance_from_start: 16 },
		{ name: 'Voisins Le Bretonneux', distance_from_start: 22 },
		{ name: 'Les Clayes-sous-Bois', distance_from_start: 34 },
		{ name: 'Beynes', distance_from_start: 42 },
		{ name: 'Marcq', distance_from_start: 47 },
		{ name: 'Hargeville', distance_from_start: 54 },
		{ name: 'Mantes-la-Ville', distance_from_start: 64 },
		{ name: 'La Roche-Guyon', distance_from_start: 84 },
		{ name: 'Gasny', distance_from_start: 87 },
		{ name: 'Vernon', distance_from_start: 96 },
		{ name: 'Tilly', distance_from_start: 103 },
		{ name: 'Vexin-sur-Epte', distance_from_start: 109 },
		{ name: 'Bray-et-Lû', distance_from_start: 115 },
		{ name: 'Ambleville', distance_from_start: 119 },
		{ name: 'Magny-en-Vexin', distance_from_start: 135 },
		{ name: 'Colombes', distance_from_start: 192 }
	];

	let current_km: number = $state(0);

	let past_checkpoints: Array<Checkpoint> = $derived(
		checkpoints.filter((e) => e.distance_from_start < current_km)
	);

	let current_checkpoint: Checkpoint = $derived(
		checkpoints.find((e) => e.distance_from_start == current_km)
	);

	let remaining_checkpoints: Array<Checkpoint> = $derived(
		checkpoints.filter((e) => e.distance_from_start > current_km)
	);

	function getFullCircles(n_km: number, n_circles_total: number): string {
		let n_full_circles: number = Math.max(
			Math.min(Math.floor(n_km / n_circles_total), n_circles_total),
			0
		);
		return '🔴'.repeat(n_full_circles);
	}

	function getEmptyCircles(n_km: number, n_circles_total: number): string {
		let n_full_circles = getFullCircles(n_km, n_circles_total).length / 2;
		let n_empty_circles: number = n_circles_total - n_full_circles;
		return '⭕'.repeat(n_empty_circles);
	}

	function set_current_km(new_km_value: number): void {
		current_km = new_km_value;
	}
</script>

{#snippet roadbookCurrentPosition()}
	<div class="flex text-center">
		<p class="grow bg-yellow-300 text-2xl">{current_checkpoint.name}: {current_km} km</p>
	</div>
{/snippet}

{#snippet roadbookItem(city, distance_km, est_passe, is_current)}
	<button
		class="my-1 flex justify-start text-center"
		class:est-passe={est_passe}
		class:bg-yellow-300={is_current}
		onclick={() => set_current_km(distance_km + current_km)}
	>
		<p class="mr-4 w-4/5 overflow-hidden text-4xl text-nowrap overflow-ellipsis">{city}</p>
		<div class="flex justify-start">
			<!--			<p class=" text-2xl">{getFullCircles(distance_km, 5)}</p>-->
			<!--			<p class="text-2xl">{getEmptyCircles(distance_km, 5)}</p>-->
		</div>
		<p
			class:opacity-20={is_current}
			class="grow rounded-lg border-2 border-solid border-red-300 bg-red-200 text-4xl font-bold"
		>
			{distance_km}
		</p>
	</button>
{/snippet}

<div class="container-roadbook">
	{#each past_checkpoints as ch}
		{@render roadbookItem(ch.name, ch.distance_from_start - current_km, true, false)}
	{/each}
	{@render roadbookItem(current_checkpoint.name, 0, false, true)}
	<!--{@render roadbookCurrentPosition()}-->
	{#each remaining_checkpoints as ch}
		{@render roadbookItem(ch.name, ch.distance_from_start - current_km, false, false)}
	{/each}
</div>

<style>
	.container-roadbook {
		display: flex;
		flex-direction: column;
	}

	p {
		margin-top: 0;
		margin-bottom: 0;
	}

	.est-passe {
		color: #5e5e5e;
		opacity: 0.2;
	}
</style>
