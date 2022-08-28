<script>

	let input = "According to a Cambridge University study, most people can read words in sentences with scrambled letters, provided the first and last letters of words are the same."
	let output;

	// update output whenever input is changed
	$: output = scrambleText(input);

	function rescramble() {
		output = scrambleText(input);
	}

	function scrambleText(text) {
		let splitText = text.split(/(?=[.\s]|\b)/);
		let scrambledText = [];
		for (let word of splitText) {

			if (word.length <= 3) {
				scrambledText.push(word);
				continue;
			}

			// remove the first and last letters
			let middleLetters = word.slice(1, -1).split("");
			
			// shuffle the letters
			let shuffledMiddleLetters = shuffle(middleLetters);

			// put the letters back together
			let scrambledWord = word.slice(0, 1) + shuffledMiddleLetters + word.slice(-1);
			scrambledText.push(scrambledWord);
		}
		return scrambledText.join("");
	}

	function shuffle(arr) {
		let newArr = [];
		while (arr.length > 0) {
			let rand = Math.floor(Math.random() * arr.length);
			newArr.push(arr[rand]);
			arr.splice(rand, 1);
		}
		return newArr.join("");
	}

</script>

<section class="section">
	<div class="container">

	<h1 class="title">Word Scrambler</h1>
	<h2 class="subtitle">Created by Zachary Robinson</h2>


	<div class="columns">
		<div class="column">
			<div class="field">
				<label class="label" for="input">Input Text</label>
				<div class="control">
					<textarea class="textarea" id="input" bind:value={input}></textarea>
				</div>
			</div>
		</div>
		<div class="column">
			<div class="field">
				<label class="label" for="output">Output Text</label>
				<div class="control">
					<textarea class="textarea" id="output" readonly>{output}</textarea>
				</div>
			</div>
			<div class="field is-grouped">
				<div class="control">
					<button class="button is-link" on:click={rescramble}>
						<span class="icon">
							<i class="fas fa-sync-alt"></i>
						</span>
						<span>Rescramble</span>
					</button>
				</div>
				<div class="control">
					<button class="button" on:click={() => navigator.clipboard.writeText(output)}>
						<span class="icon">
							<i class="far fa-copy"></i>
						</span>
						<span>Copy</span>
					</button>
				</div>
			</div>
		</div>
	</div>

	</div>
</section>

<style>
</style>
