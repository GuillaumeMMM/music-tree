<script lang="ts">
	import { SvelteFlow, type Edge, type Node } from '@xyflow/svelte';

	import '@xyflow/svelte/dist/style.css';

	let nodes = $state.raw(
		[
			{
				id: '1',
				position: { x: 500, y: 0 },
				data: {
					label: 'Selected Ambient Works 85-92',
					imageUrl:
						'https://cdn-images.dzcdn.net/images/cover/61597432632bf90678b7132db0451f45/250x250-000000-80-0-0.jpg'
				}
			},
			{
				id: '2',
				position: { x: 200, y: 0 },
				data: {
					label: 'Selected Ambient Works Volume II',
					imageUrl:
						'https://cdn-images.dzcdn.net/images/cover/a56fa0f134499988714bb5bfcf1d2f71/500x500-000000-80-0-0.jpg'
				}
			},
			{
				id: '3',
				position: { x: 800, y: 0 },
				data: {
					label: 'Surfing on Sine Waves',
					imageUrl:
						'https://cdn-images.dzcdn.net/images/cover/fd2872189c9cf1304d34785a350db5a3/500x500-000000-80-0-0.jpg'
				}
			},
			{
				id: '4',
				position: { x: 300, y: 300 },
				data: {
					label: '...I Care Because You Do',
					imageUrl:
						'https://cdn-images.dzcdn.net/images/cover/5cd2fa04adfb4248c3d7e1f612b5c7fd/500x500-000000-80-0-0.jpg'
				}
			},
			{
				id: '5',
				position: { x: 700, y: 300 },
				data: {
					label: 'Richard D. James Album',
					imageUrl:
						'https://cdn-images.dzcdn.net/images/cover/3aa42e96e2c621d7e4caf305812a6398/500x500-000000-80-0-0.jpg'
				}
			},
			{
				id: '6',
				position: { x: 700, y: 500 },
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
			selectable: false
		})) satisfies Node[]
	);

	let edges = $state.raw(
		[
			{ id: 'e1-2', source: '1', target: '2', label: 'I want less beats and more atmosphere' },
			{ id: 'e1-3', source: '1', target: '3' },
			{ id: 'e1-4', source: '1', target: '4', label: 'I want something noisier' },
			{ id: 'e1-5', source: '1', target: '5', label: 'I want something much more upbeat' },
			{ id: 'e5-6', source: '5', target: '6' }
		].map((e) => ({
			...e,
			deletable: false,
			selectable: false,
			focusable: false,
			labelStyle: 'label'
		})) satisfies Edge[]
	);
</script>

<div style:width="100vw" style:height="100vh">
	<SvelteFlow bind:nodes bind:edges />
</div>

<style>
	:global {
		.svelte-flow__edge-label {
			background-color: red;
			max-width: 100px;
			color: white;
		}
	}
</style>
