<script lang="ts">
	import { onDestroy, onMount } from 'svelte';
	import type { Content } from '@tiptap/core';
	import { Editor } from '@tiptap/core';
	import StarterKit from '@tiptap/starter-kit';

	let editor = $state<Editor>();
	let element = $state<HTMLElement>();

	let {
		content = $bindable(null)
	}: {
		content: Content;
	} = $props();

	onMount(() => {
		editor = new Editor({
			element,
			content,
			extensions: [
                StarterKit,
            ],
			editorProps: {
				attributes: {
					// @tailwindcss/typography をインストールしている場合に使えるクラス
					class: 'prose max-w-full'
				}
			},
			onTransaction: ({ editor }) => {
				content = editor.getJSON();
			}
		});
	});

	onDestroy(() => {
		if (editor) {
			editor.destroy();
		}
	});
</script>

<div bind:this={element} class="border-2"></div>
