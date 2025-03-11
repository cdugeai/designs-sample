<script lang="ts">
	import CodeMirror from 'svelte-codemirror-editor';
	import { javascript } from '@codemirror/lang-javascript';
	import { json } from '@codemirror/lang-json';
	import { linter } from '@codemirror/lint';

	let { value = $bindable() } = $props();
</script>

<!-- TODO: Add linter to CodeMirror object -->
<CodeMirror bind:value lang={json()} extensions={[json()]} />
