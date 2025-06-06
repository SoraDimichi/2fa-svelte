<script lang="ts">
	type ButtonProps = {
		isComplete: boolean;
		isCorrect: boolean;
		index: number;
		numbers: string[];
		handleKeyNavigation: (index: number) => (event: KeyboardEvent) => void;
		handleInput: (index: number) => (event: any) => void;
	};
	let isFocused = $state(false);
	const { isComplete, isCorrect, index, handleKeyNavigation, handleInput, numbers }: ButtonProps =
		$props();
</script>

<div
	class={`group relative flex h-12 w-10 items-center justify-center overflow-hidden rounded-lg border ${!numbers[index] ? 'border-[#798694]' : 'border-[#3C8AC6]'} px-3 text-2xl ${
		isComplete && !isCorrect
			? 'border-rose-500 bg-[#FEF7F6] text-rose-500'
			: 'text-[#3C8AC6]  focus-within:border-[#3C8AC6]'
	}`}
>
	<input
		id={`Input${index}`}
		class="no-cursor h-full w-full translate-y-[0%] transform border-[#3c8ac6] text-transparent transition-transform duration-500 ease-out focus:translate-y-[-15%] focus:border-b focus:outline-none"
		type="number"
		maxlength="1"
		onfocus={() => (isFocused = true)}
		onblur={() => (isFocused = false)}
		oninput={(event: any) => {
			if (!event.target) return;
			const value = event.target?.value.slice(0, 1);
			handleInput(index)(value);
			event.target.value = value;
		}}
		onkeydown={handleKeyNavigation(index)}
	/>
	<span
		class={`no-cursor m-t-2 absolute inset-0 bottom-0 z-0 h-full w-full text-center align-middle leading-[200%] transition-transform duration-500 ease-out
		${isComplete && !isCorrect ? 'bg-[#FEF7F6] text-rose-500' : 'text-[#3C8AC6]'}
		${numbers[index] ? 'translate-y-0' : 'translate-y-[-100%]'}`}
	>
		{numbers[index]}
	</span>
</div>

<style>
	.no-cursor {
		caret-color: transparent;
	}
	input[type='number']::-webkit-inner-spin-button,
	input[type='number']::-webkit-outer-spin-button {
		-webkit-appearance: none;
		margin: 0;
	}
</style>
