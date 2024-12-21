<script lang="ts">
	import { onDestroy, onMount } from 'svelte';
	import type { Content } from '@tiptap/core';
	import { Editor } from '@tiptap/core';
	import StarterKit from '@tiptap/starter-kit';
	import { SvelteCounterExtension } from './SvelteExtension';

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
                SvelteCounterExtension, // Counter拡張機能として追加
            ],
			editorProps: {
				attributes: {
					// @tailwindcss/typography をインストールしている場合に使えるクラス
					class: 'prose max-w-full'
				}
			},
			onTransaction: (transaction) => {
                editor = transaction.editor;
                content = editor.getJSON();
			}
		});
	});

	onDestroy(() => {
		if (editor) {
			editor.destroy();
		}
	});

    const addCounter = () => {
        if (!editor) return;
        // editorインスタンスにSvelteCounterComponentを挿入
		editor
			.chain()
			.insertContent({
				type: 'SvelteCounterComponent',
			})
			.focus()
			.run();
	}
</script>

<button onclick={addCounter} class="bg-blue-500 text-white px-4 py-2 rounded">
    カウンターを追加
</button>

<div bind:this={element} class="border-2"></div>
