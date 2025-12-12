<script lang="ts">
	import { Handle, Position, type NodeProps } from '@xyflow/svelte';

	let { id, data }: NodeProps = $props();
</script>

<div class="album nodrag nopan">
	<img alt={data.label as string} src={data.imageUrl as string} class="album-cover" />
	<p class="album-name">{data.label}</p>
</div>

{#each data.connectedHandles as string[] as handleId}
	<Handle
		type={handleId.split('-')[0] as 'source' | 'target'}
		position={handleId.split('-')[1] as Position}
		id={handleId}
	/>
{/each}

<style>
	.album {
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 5px;
	}

	.album-cover {
		width: 150px;
		height: 150px;
	}

	.album-name {
		max-width: 200px;
		text-align: center;
	}
</style>
