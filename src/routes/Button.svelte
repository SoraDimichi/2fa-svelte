<script lang="ts">
	type ButtonProps = { isComplete: boolean; isCorrect: boolean; numbers: string[] };
	const { isComplete, isCorrect, numbers }: ButtonProps = $props();
</script>

<button
	class={`group bg-[#ECEEF1] relative mt-6 w-full overflow-hidden rounded-md p-3 text-center transition-colors duration-300 hover:text-white ${
		isComplete ? 'text-white' : 'text-[#798694]'
	}`}
>
	<span class="relative z-1">
		{#if isComplete}
			{#if isCorrect}
				Let's go!
			{:else}
				Wrong code!
			{/if}
		{:else}
			{6 - numbers.filter((n) => n !== '').length} digits left
		{/if}
	</span>
	<span
		class={`absolute inset-0 z-0 origin-right  transform ${isComplete ? (isCorrect ? 'scale-x-100 bg-blue-600 bg-black transition-transform duration-300' : 'bg-red-600') : 'scale-x-0'}`}
	></span>
</button>
