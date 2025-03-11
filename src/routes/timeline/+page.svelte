<script lang="ts">
	interface Etape {
		start: string;
		place: string;
	}

	interface Duration {
		days: number;
		and_hours: number;
	}

	interface EtapeCalculs {
		start: string;
		place: string;
		duration: Duration;
		is_current: boolean;
		is_complete: boolean;
	}

	function getIsComplete(e: Etape, next_e: Etape): boolean {
		if (next_e === undefined) {
			return false;
		}
		let nnow: Date = new Date();
		return nnow > new Date(next_e.start);
	}

	function getIsCurrent(e: Etape, next_e: Etape): boolean {
		let nnow: Date = new Date();
		if (next_e === undefined) {
			return nnow > new Date(e.start);
		}
		return nnow < new Date(next_e.start) && nnow > new Date(e.start);
	}

	function getDuration(e: Etape, next_e: Etape | undefined): Duration {
		if (next_e === undefined) {
			return {
				days: -1,
				and_hours: -1
			};
		}
		let duration_ms: number = new Date(next_e.start).getTime() - new Date(e.start).getTime();
		let duration_min: number = duration_ms / 60000;
		let duration_days: number = Math.floor(duration_min / 1440);
		let duration_and_hours: number = (duration_min - duration_days * 1440) / 60;

		return {
			days: duration_days,
			and_hours: duration_and_hours
		};
	}

	const etapes: Etape[] = [
		{ place: 'Paris', start: '03/08/2025 08:00:00' },
		{ place: 'Bordeaux', start: '03/11/2025 02:00:00' },
		{ place: 'Toulouse', start: '03/12/2025 08:00:00' }
	];

	const etapesCal: EtapeCalculs[] = etapes.map((e, index) => {
		let duration_e: Duration = getDuration(e, etapes[index + 1]);
		return {
			place: e.place,
			start: e.start,
			duration: {
				days: duration_e.days,
				and_hours: duration_e.and_hours
			},
			is_complete: getIsComplete(e, etapes[index + 1]),
			is_current: getIsCurrent(e, etapes[index + 1])
		};
	});

	function formatDate(date_ts: string): string {
		let dd: Date = new Date(date_ts);
		let month: string = String(dd.getMonth() + 1).padStart(2, '0');
		let dday: string = String(dd.getDate()).padStart(2, '0');
		let hhours: string = String(dd.getHours()).padStart(2, '0');
		let mminutes: string = String(dd.getMinutes()).padStart(2, '0');
		return `${dday}/${month} ${hhours}h${mminutes}`;
	}
</script>

{#snippet rond()}
	<div class="continuous-line fixed-h"></div>
	<svg class="continuous-line hide" width="35" height="50" xmlns="http://www.w3.org/2000/svg">
		<g id="Layer_1">
			<title>Layer 1</title>
			<ellipse
				class="svg-style"
				ry="15"
				rx="14.62506"
				id="svg_1"
				cy="25.375"
				cx="17.75009"
				fill="#fff"
			/>
			<line
				id="svg_2"
				y2="49.875"
				x2="17.62507"
				y1="-0.125"
				x1="17.62507"
				class="svg-style"
				fill="none"
			/>
		</g>
	</svg>
{/snippet}

{#snippet dot()}
	<svg class="dot" height="10" width="10" xmlns="http://www.w3.org/2000/svg">
		<circle r="5" cx="5" cy="5" />
		Sorry, your browser does not support inline SVG.
	</svg>
{/snippet}

{#snippet bloc(place: string, date_: string, duration: Duration, is_complete: boolean)}
	<div class="flex flex-row items-center">
		{@render rond()}
		{@render dot()}

		<p class="bloc-date" class:is-complete={is_complete}>{formatDate(date_)}</p>
		<p class="bloc-city" class:is-complete={is_complete}>{place}</p>
		<div
			class="bloc-duration hide"
			class:is-complete={is_complete}
			class:show={duration.days > 0 || duration.and_hours > 0}
		>
			<span>(</span>
			<span class="hide" class:show={duration.days > 0}>
				{duration.days}d,
			</span>
			<span class="hide" class:show={duration.and_hours > 0}>
				{duration.and_hours}h
			</span>
			<span>)</span>
		</div>
	</div>
{/snippet}

<div class="mx-3 flex max-w-xl flex-col gap-0">
	{#each etapesCal as etape}
		{@render bloc(etape.place, etape.start, etape.duration, etape.is_complete)}
		{console.log(etape)}
	{/each}
</div>

<style>
	p {
		margin: 0;
	}

	.svg-style {
		stroke: #0a3aa1;
		stroke-width: 2;
	}

	.dot {
		margin: 0 0 0 0;
		padding: 0 0 0 0;
		position: relative;
		top: 0;
		left: 0;
		translate: -14px;
		fill: #0772bd;
	}

	.continuous-line {
		padding-left: 0.5rem;
		border-left: #0772bd 2px solid;
	}
	.fixed-h {
		height: 40px;
	}

	.bloc-date {
		font-style: italic;
		margin-left: 2vw;
		width: 20%;
		text-wrap: nowrap;
	}
	.is-complete {
		opacity: 0.4;
	}
	.bloc-city {
		font-size: 1rem;
		font-weight: bold;
		margin-right: 0.5rem;
		margin-left: 1rem;
		width: 20%;
	}
	.bloc-duration {
		gap: 0;
		column-gap: 0;
		width: 30%;
		text-wrap: nowrap;
	}
	.hide {
		display: none;
	}
	.show {
		display: inline-block;
	}
</style>
