<script lang="ts">

	const title: string = 'Roadbook';

	interface Checkpoint {
		name: string;
		distance_from_start: number;
	}

	const checkpoints: Array<Checkpoint> = [
		{ name: 'Clamart', distance_from_start: 0 },
		{ name: 'Jouy-en-Josas', distance_from_start: 8 },
		{ name: 'Chevreuse', distance_from_start: 21 },
		{ name: 'Auffargis', distance_from_start: 32 },
		{ name: 'Condé-sur-Vesgre', distance_from_start: 50 },
		{ name: 'Adainville', distance_from_start: 53 },
		{ name: 'Saint-Léger-en-Yvelines', distance_from_start: 62 },
		{ name: 'Le Perray-en-Yvelines', distance_from_start: 69 },
		{ name: 'Bullion', distance_from_start: 82 },
		{ name: 'Limours', distance_from_start: 90 },
		{ name: 'Janvry', distance_from_start: 96 },
		{ name: 'Marcoussis', distance_from_start: 102 },
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
		<p class="w-4/5 text-4xl text-nowrap overflow-ellipsis overflow-hidden mr-4 ">{city}</p>
		<div class="flex justify-start">
			<!--			<p class=" text-2xl">{getFullCircles(distance_km, 5)}</p>-->
			<!--			<p class="text-2xl">{getEmptyCircles(distance_km, 5)}</p>-->
		</div>
		<p
			class:opacity-20={is_current}
			class="grow rounded-lg border-2 border-solid border-red-300 bg-red-200 text-4xl font-bold">
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
