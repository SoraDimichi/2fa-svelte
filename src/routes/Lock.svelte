<script lang="ts">
	type LockProps = { isComplete: boolean; isCorrect: boolean };
	const { isComplete, isCorrect }: LockProps = $props();
</script>

<div class="group relative flex h-20 w-20 items-center justify-center rounded-full">
	<svg
		height="40"
		class={`z-2 translate-x-[15%] ${isComplete && 'animate-lock'}`}
		viewBox="0 0 354 370"
		fill="none"
		xmlns="http://www.w3.org/2000/svg"
		stroke={!isComplete ? '#0794ff' : isCorrect ? '#1AAF82' : '#FD4B63'}
	>
		<circle cx="125" cy="240" r="119" stroke-width="12" />
		<line x1="199" y1="83" x2="198" y2="143" stroke-width="12" />
		{#if !(isComplete && isCorrect)}
			<line x1="50" y1="88" x2="50" y2="148" stroke-width="12" />
			<path d="M199 88C199 44.9 165.6 10 124.5 10C83.35 10 50 44.9 50 88" stroke-width="12" />
		{:else}
			<line y1="-6" x2="60" y2="-6" transform="matrix(0 1 1 0 354 84)" stroke-width="12" />
			<path d="M199 84C199 40.9 232.4 6 273.5 6C314.6 6 348 40.9 348 84" stroke-width="12" />
		{/if}
		<circle cx="125" cy="213" r="10" stroke-width="12" />
		<line x1="125" y1="227" x2="125" y2="277" stroke-width="12" />
	</svg>
	<div
		class={`absolute inset-0 z-1 flex h-20 w-20 rounded-full ${isComplete ? (isCorrect ? 'bg-green-100' : 'bg-rose-100') : 'bg-[#E8F5FF]'}`}
	></div>
	{#if isComplete}
		<div
			class={`absolute inset-0 z-0 flex h-20 w-20 rounded-full animate-wave ${isCorrect ? 'bg-green-50' : 'bg-rose-50'}`}
		></div>
	{/if}
</div>

<style>
	@keyframes lesser-pulse {
		0% {
			transform: scale(1);
		}
		50% {
			transform: scale(1.2);
		}
		100% {
			transform: scale(1);
		}
	}

	@keyframes pulse {
		0% {
			transform: scale(1);
		}
		100% {
			transform: scale(1.5);
		}
	}

	.animate-lock {
		animation: lesser-pulse 0.5s;
	}

	.animate-wave {
		animation: pulse 0.5s ease-out;
	}
</style>
