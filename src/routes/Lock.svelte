<script lang="ts">
	type LockProps = { isComplete: boolean; isCorrect: boolean };
	const { isComplete, isCorrect }: LockProps = $props();
</script>

<div class="group relative flex h-20 w-20 items-center justify-center rounded-full">
	<div class="group relative z-2 mt-4">
		<svg
			fill={!isComplete ? '#0794ff' : isCorrect ? '#1AAF82' : '#FD4B63'}
			xmlns="http://www.w3.org/2000/svg"
			width="30"
			viewBox="0 0 250 250"
		>
			<path
				d="M238 125C238 62.5918 187.408 12 125 12C62.5918 12 12 62.5918 12 125C12 187.408 62.5918 238 125 238C187.408 238 238 187.408 238 125ZM129 98C129 95.7909 127.209 94 125 94C122.791 94 121 95.7909 121 98C121 100.209 122.791 102 125 102C127.209 102 129 100.209 129 98ZM250 125C250 194.036 194.036 250 125 250C55.9644 250 0 194.036 0 125C0 55.9644 55.9644 0 125 0C194.036 0 250 55.9644 250 125ZM141 98C141 104.714 136.863 110.461 131 112.835V162H119V112.835C113.137 110.461 109 104.714 109 98C109 89.1634 116.163 82 125 82C133.837 82 141 89.1634 141 98Z"
			/>
		</svg>
		<div
			class={`absolute top-[-15px] right-[5px] z-3 grid h-[1px] w-[1px] items-start ${isComplete && isCorrect && 'animate-unlocks'}`}
		>
			<svg
				fill={!isComplete ? '#0794ff' : isCorrect ? '#1AAF82' : '#FD4B63'}
				xmlns="http://www.w3.org/2000/svg"
				height="19"
				viewBox="0 0 161 144"
				class="ml-[-20px]"
			>
				<path
					d="M0 84C0 37.848 35.7805 0 80.5 0C123.574 0 158.431 35.1951 160.862 79.0967L160.999 79.0996L160.96 81.4062C160.985 82.2678 161 83.1324 161 84H160.917L159.999 139.1L148.001 138.9L148.957 81.4834C147.692 42.6243 117.243 12 80.5 12C42.9195 12 12 43.952 12 84V144H0V84Z"
				/>
			</svg>
		</div>
	</div>
	<div
		class={`absolute inset-0 z-1 flex h-20 w-20 rounded-full ${isComplete ? (isCorrect ? 'bg-green-100' : 'bg-rose-100') : 'bg-[#E8F5FF]'}`}
	></div>
	{#if isComplete}
		<div
			class={`animate-wave absolute inset-0 z-0 flex h-20 w-20 rounded-full ${isCorrect ? 'bg-green-50' : 'bg-rose-50'}`}
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

	@keyframes unlocks {
		0% {
			transform: scaleX(0);
		}
		100% {
			transform: scaleX(-1);
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

	.animate-unlocks {
		animation: unlocks 0.5s forwards;
	}

	.animate-lock {
		animation: lesser-pulse 0.5s;
	}

	.animate-wave {
		animation: pulse 0.5s ease-out;
	}
</style>
