<script lang="ts"></script>

{#snippet item(title: string, href: string)}
	<li>
		{title}
		<a
			{href}
			class="inline-flex items-center font-medium text-blue-600 hover:underline dark:text-blue-500"
		>
			See
			<svg
				class="ms-2 h-4 w-4 rtl:rotate-180"
				aria-hidden="true"
				xmlns="http://www.w3.org/2000/svg"
				fill="none"
				viewBox="0 0 14 10"
			>
				<path
					stroke="currentColor"
					stroke-linecap="round"
					stroke-linejoin="round"
					stroke-width="2"
					d="M1 5h12m0 0L9 1m4 4L9 9"
				/>
			</svg>
		</a>
	</li>
{/snippet}

<div class="container">
	<h1 class="main-title mb-10 ml-5 text-4xl font-extrabold">Design samples</h1>

	<p class="my-4 text-lg text-gray-500">Some sample designs using CSS, Tailwind, Svelte.</p>

	<ul class="list-disc pl-10">
		{@render item('🛵 Motorbike roadbook', '/roadbook')}
		{@render item('🥅 A simple score panel', '/score-panel')}
		{@render item('🌴 A simple travel timeline', '/timeline')}
	</ul>
</div>

<style>
	.container {
		display: flex;
		flex-direction: column;
		margin-left: 5%;
		margin-top: 1rem;
		width: 90%;
	}
</style>
