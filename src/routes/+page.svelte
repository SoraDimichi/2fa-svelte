<script lang="ts">
	import '../app.css';
	import Button from './Button.svelte';
	import Input from './Input.svelte';
	import Lock from './Lock.svelte';

	import { CORRECT } from './const';
	$effect(() => document.getElementById('Input0')?.focus());

	let numbers = $state(Array(6).fill(''));

	const handleInput = (index: number) => (value: string) => {
		numbers[index] = value || '';
		if (value && index < 5) document.getElementById(`Input${index + 1}`)?.focus();
	};

	const handleKeyNavigation = (index: number) => (event: KeyboardEvent) => {
		const { key } = event;

		if (key === 'Backspace') {
			if (!numbers[index] && index > 0) document.getElementById(`Input${index - 1}`)?.focus();
			numbers[index] = '';
		} else if (key === 'ArrowLeft' && index > 0) {
			document.getElementById(`Input${index - 1}`)?.focus();
		} else if (key === 'ArrowRight' && index < 5) {
			document.getElementById(`Input${index + 1}`)?.focus();
		}
	};

	const isComplete = $derived(numbers.every((n) => n !== ''));
	const isCorrect = $derived(numbers.join('') === CORRECT);
</script>

<div class="flex h-screen w-screen items-center justify-center bg-[#E4F4FF] font-sans">
	<div class="flex flex-col items-center justify-center rounded-xl bg-white p-8 shadow-xl">
		<Lock {isComplete} {isCorrect} />
		<div class="mt-4 text-4xl font-semibold">Easy peasy</div>
		<div class="mt-4 text-xs text-[#7A8496]">
			Enter 6-digit code from your two-factor authenticator APP.
		</div>
		<div class={isComplete && !isCorrect ? 'animate-shake' : ''}>
			<div class="mt-8 flex gap-2">
				{#each numbers, index}
					<Input {numbers} {index} {handleInput} {handleKeyNavigation} {isComplete} {isCorrect} />
				{/each}
			</div>
			<Button {isComplete} {numbers} {isCorrect} />
		</div>
	</div>
</div>

<style>
	@keyframes shake {
		0% {
			transform: translate(0, 0) rotate(0deg);
		}
		25% {
			transform: translate(-1px, 1px) rotate(-0.5deg);
		}
		50% {
			transform: translate(1px, -1px) rotate(0.5deg);
		}
		75% {
			transform: translate(-1px, 0.5px) rotate(0deg);
		}
		100% {
			transform: translate(0.5px, -1px) rotate(-0.5deg);
		}
	}

	.animate-shake {
		animation: shake 0.5s;
	}
</style>
