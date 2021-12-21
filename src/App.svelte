<script>
	export let name;
	export let size;
	export let pairs = [];
	export let showPairs = false;
	export let showOddWarning = false;
	export let showLessWarning = false;

	const isOdd = (num) => { return num % 2;}

	const range = (start, end) => {
		const ranger = [];
		for (let i=start; i <=end; i++) {
			console.log(i);
			ranger.push(i);
		}
		return ranger;
	}

	function shuffle(arr) {
  		return arr.sort(() => Math.random() - 0.5);
	}

	const match = (size) => {
		const people_number = shuffle(range(1, size));
		const pairs = [];
		if (isOdd(size)) {
			pairs.push(`${people_number.pop()} - ${people_number.pop()}-${people_number.pop()}`);
			showOddWarning = true;
		}
		while (people_number.length !== 0) {
			let el1 = people_number.pop();
			let el2 = people_number.pop();
			pairs.push(`${el1} - ${el2}`)
		}
		return pairs;
	}

	const generatePairs = (size) => {
		if (size < 3) {
			showLessWarning = true;
		} else {
			pairs = match(size);
			showPairs = true;
		}
	}

	const reset = () => {
		pairs = [];
		showPairs = false;
		showOddWarning = false;
	}
</script>

<main>
	<h1>请输入人数</h1>
	<input type=number bind:value={size} min=1>
	<button on:click={generatePairs(size)}>配对</button>
	<button on:click={reset}>重置</button>
	<p style="display: {showOddWarning ? 'block' : 'none'};">奇数组合，请三人组合互相交换礼物</p>
	<p style="display: {showLessWarning ? 'block' : 'none'}; color: #ff3e00;">请输入>3整数</p>
	<div style="display: {showPairs ? 'block' : 'none'};">
		{#each pairs as p}
		<p>{p}</p>
		{/each}
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>