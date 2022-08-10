<script lang="ts">
	import { clipboard } from '$lib/actions/useClipboard';
	import { fly } from 'svelte/transition';
	import { cubicIn, cubicOut } from 'svelte/easing';

	let isActive = false;
	let timer: ReturnType<typeof setTimeout>;

	const runTimer = () => {
		timer = setTimeout(() => {
			isActive = false;
		}, 1500);
	};

	export const toggleToast = () => {
		isActive = true;
		clearTimeout(timer);
		runTimer();
	};

	const path: string =
		'M13 20h2a3 3 0 0 1-6 0h2a1 1 0 0 0 2 0Zm8-5v3a1 1 0 0 1-1 1H4a1 1 0 0 1-1-1v-3a1 1 0 0 1 .29-.71L5 12.59V8a7 7 0 0 1 14 0v4.59l1.71 1.7A1 1 0 0 1 21 15Zm-2 .41-1.71-1.7A1 1 0 0 1 17 13V8A5 5 0 0 0 7 8v5a1 1 0 0 1-.29.71L5 15.41V17h14Z';
</script>

<section
	class="relative flex justify-center items-center w-screen h-screen bg-gradient-to-r from-pink-300 via-purple-300 to-indigo-400"
>
	<button
		class="grid group relative"
		type="button"
		use:clipboard={path}
		on:useclipboard={toggleToast}
	>
		<div
			class="relative flex flex-col gap-y-2 text-white bg-gray-800/40 border border-gray-800/10 rounded shadow group-hover:text-blue-600 group-hover:bg-white/80 group-hover:border-blue-600 group-hover:shadow-2xl group-hover:-translate-y-2 p-6 pb-4 transition-all duration-500 ease-out"
		>
			<div class="p-4">
				<svg
					class="w-12"
					xmlns="http://www.w3.org/2000/svg"
					viewBox="0 0 24 24"
					xml:space="preserve"
					><path d={path} fill="currentColor" />
				</svg>
			</div>
			<div class="flex flex-col items-center w-full">
				<p class="font-semibold text-sm text-center w-full">Alarm</p>
			</div>
		</div>
	</button>

	{#if isActive}
		<div
			class="absolute bottom-8 left-1/2 -translate-x-1/2 text-white bg-gray-900 py-2 px-4 rounded"
			in:fly={{ y: 20, easing: cubicOut }}
			out:fly={{ y: 20, easing: cubicIn }}
		>
			SVG Copied
		</div>
	{/if}
</section>
