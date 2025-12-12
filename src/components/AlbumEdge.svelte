<script lang="ts">
	import { BaseEdge, EdgeLabel, getBezierPath, useEdges, type EdgeProps } from '@xyflow/svelte';

	let { id, sourceX, sourceY, targetX, targetY, label }: EdgeProps = $props();

	let [edgePath, labelX, labelY] = $derived(
		getBezierPath({
			sourceX,
			sourceY,
			targetX,
			targetY,
			curvature: 0
		})
	);

	const edges = useEdges();
</script>

<BaseEdge {id} path={edgePath} />

{#if label}
	<EdgeLabel x={labelX} y={labelY}>
		<p class="edge-label nodrag nopan">{label}</p>
	</EdgeLabel>
{/if}

<style>
	.edge-label {
		max-width: 100px;
	}
</style>
