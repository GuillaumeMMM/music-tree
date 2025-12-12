<script lang="ts">
	import { SvelteFlow, type Edge, type EdgeTypes, type Node } from '@xyflow/svelte';

	import '@xyflow/svelte/dist/style.css';
	import AlbumNode from '../../components/AlbumNode.svelte';
	import AlbumEdge from '../../components/AlbumEdge.svelte';

	const nodeTypes = { album: AlbumNode };

	const edgeTypes: EdgeTypes = {
		'album-edge': AlbumEdge
	};

	let edges = $state.raw(
		[
			{
				id: 'e1-2',
				source: '1',
				target: '2',
				label: 'I want less beats and more atmosphere',
				sourceHandle: 'source-left',
				targetHandle: 'target-right'
			},
			{
				id: 'e1-3',
				source: '1',
				target: '3',
				sourceHandle: 'source-right',
				targetHandle: 'target-left'
			},
			{
				id: 'e1-4',
				source: '1',
				target: '4',
				label: 'I want something noisier',
				sourceHandle: 'source-bottom',
				targetHandle: 'target-top'
			},
			{
				id: 'e1-5',
				source: '1',
				target: '5',
				label: 'I want something much more upbeat',
				sourceHandle: 'source-bottom',
				targetHandle: 'target-top'
			},
			{
				id: 'e5-6',
				source: '5',
				target: '6',
				sourceHandle: 'source-bottom',
				targetHandle: 'target-top'
			}
		].map((e) => ({
			...e,
			deletable: false,
			selectable: false,
			focusable: false,
			type: 'album-edge'
		})) satisfies Edge[]
	);

	let nodes = $state.raw(
		[
			{
				id: '1',
				position: { x: 500, y: 50 },
				data: {
					label: 'Selected Ambient Works 85-92',
					imageUrl:
						'https://cdn-images.dzcdn.net/images/cover/61597432632bf90678b7132db0451f45/250x250-000000-80-0-0.jpg'
				}
			},
			{
				id: '2',
				position: { x: 100, y: 50 },
				data: {
					label: 'Selected Ambient Works Volume II',
					imageUrl:
						'https://cdn-images.dzcdn.net/images/cover/a56fa0f134499988714bb5bfcf1d2f71/500x500-000000-80-0-0.jpg'
				}
			},
			{
				id: '3',
				position: { x: 900, y: 50 },
				data: {
					label: 'Surfing on Sine Waves',
					imageUrl:
						'https://cdn-images.dzcdn.net/images/cover/fd2872189c9cf1304d34785a350db5a3/500x500-000000-80-0-0.jpg'
				}
			},
			{
				id: '4',
				position: { x: 300, y: 350 },
				data: {
					label: '...I Care Because You Do',
					imageUrl:
						'https://cdn-images.dzcdn.net/images/cover/5cd2fa04adfb4248c3d7e1f612b5c7fd/500x500-000000-80-0-0.jpg'
				}
			},
			{
				id: '5',
				position: { x: 700, y: 350 },
				data: {
					label: 'Richard D. James Album',
					imageUrl:
						'https://cdn-images.dzcdn.net/images/cover/3aa42e96e2c621d7e4caf305812a6398/500x500-000000-80-0-0.jpg'
				}
			},
			{
				id: '6',
				position: { x: 700, y: 550 },
				data: {
					label: 'Girl/Boy EP',
					imageUrl:
						'https://cdn-images.dzcdn.net/images/cover/eb386a3fac37d1f7e8c447fa3b8b64de/500x500-000000-80-0-0.jpg'
				}
			}
		].map((n) => ({
			...n,
			draggable: false,
			connectable: false,
			deletable: false,
			selectable: false,
			type: 'album',
			data: {
				...n.data,
				connectedHandles: Array.from(
					new Set(
						edges
							.filter((e) => e.id.startsWith(`e${n.id}-`) || e.id.endsWith(`-${n.id}`))
							.filter((e) => e.sourceHandle || e.targetHandle)
							.map((e) => (e.id.startsWith(`e${n.id}-`) ? e.sourceHandle : e.targetHandle))
					)
				)
			}
		})) satisfies Node[]
	);
</script>

<div style:width="100vw" style:height="100vh">
	<SvelteFlow bind:nodes bind:edges {edgeTypes} {nodeTypes} />
</div>
