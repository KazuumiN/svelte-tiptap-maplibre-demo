<script lang="ts">
	import Editor from '$lib/Editor.svelte';
	import type { Content } from '@tiptap/core';
	let content = $state<Content>(null);
</script>

<Editor bind:content />
