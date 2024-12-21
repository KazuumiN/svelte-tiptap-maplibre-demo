<script lang="ts">
	import type { NodeViewProps } from '@tiptap/core';
	import { NodeViewWrapper } from 'svelte-tiptap';

	let { node, updateAttributes }: NodeViewProps = $props();

	const handleClick = () => {
		// クリックしたときに、属性の count を1増やす
		updateAttributes({ count: node.attrs.count + 1 });
	};
</script>

<NodeViewWrapper class="border-2 border-green-400">
	<span>スベルトコンポーネント</span>
	<div>
		<button onclick={handleClick} type="button">
			クリック数: {node.attrs.count}回
		</button>
	</div>
</NodeViewWrapper>
