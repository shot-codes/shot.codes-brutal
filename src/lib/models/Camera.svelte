<!--
Auto-generated by: https://github.com/threlte/threlte/tree/main/packages/gltf
Command: npx @threlte/gltf@2.0.1 models/camera/camera.gltf --transform
-->

<script>
	import { Group, MeshBasicMaterial } from 'three';
	import { T, forwardEventHandlers } from '@threlte/core';
	import { useGltf } from '@threlte/extras';
	import { colorScheme } from '$lib/stores';

	export const ref = new Group();

	const gltf = useGltf('/models/camera-transformed.glb', { useDraco: true });

	const component = forwardEventHandlers();

	const wireMaterialDark = new MeshBasicMaterial({
		color: 0xffffff,
		wireframe: true
	});

	const wireMaterialLight = new MeshBasicMaterial({
		color: 0x000000,
		wireframe: true
	});

	let material = wireMaterialDark;

	$: {
		if ($colorScheme == 'dark') {
			material = wireMaterialDark;
		}
		if ($colorScheme == 'light') {
			material = wireMaterialLight;
		}
	}
</script>

<T is={ref} dispose={false} {...$$restProps} bind:this={$component}>
	{#await gltf}
		<slot name="fallback" />
	{:then gltf}
		<T.Mesh
			geometry={gltf.nodes.Camera.geometry}
			{material}
			position={[0, 2.03, 1.16]}
			scale={[-0.25, -0.03, -0.25]}
		/>
	{:catch error}
		<slot name="error" {error} />
	{/await}

	<slot {ref} />
</T>
