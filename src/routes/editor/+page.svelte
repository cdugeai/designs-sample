<script lang="ts">
	import CodeEditor from '$lib/components/CodeEditor.svelte';

	const initialValue: object = {
		bob: 12,
		martine: 45
	};
	let editorValueString = $state(JSON.stringify(initialValue, null, 2));

	$inspect(editorValueString);
</script>

<div class="m-8">
	<h1 class="mb-3">Code editor</h1>
	<CodeEditor bind:value={editorValueString} />

	<div class="flex flex-col">
		<p>{JSON.stringify(JSON.parse(editorValueString), null, 4)}</p>
	</div>
</div>
