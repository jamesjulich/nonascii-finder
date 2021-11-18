<script>
	const regex = /[^\x00-\xFF]/gu;

	let input = "";
	$: matches = findMatches(input);

	let findMatches = function(text) {
		matches = [];
		let lines = text.split("\n");
		for (let i = 0; i < lines.length; i++) {
			let found = lines[i].match(regex);
			//console.log(found);
			if (found != null && found.length != 0) {
				matches.push({line: i + 1, values: found});
			}
		}
		return matches;
	}
</script>

<main>
	<div class="container">
		<h1>Non-ASCII Finder</h1>
		<textarea placeholder="Paste your text here..." bind:value={input} />
		{#if matches.length != 0}
		<h2>Invalid characters: </h2>
		{#each matches as match}
			<p>Line {match.line}:
				{#each match.values as value}
					{value}&nbsp
				{/each}
			</p>
		{/each}
	{/if}
	</div>
</main>
<footer>
	<p>Made by James Julich - <a href="https://github.com/jamesjulich/nonascii.github.io">Github</a></p>
</footer>

<style>
	main {
		padding: 1em;
		margin: auto;
		width: 80vw;
	}

	footer {
		width: 80vw;
		margin: auto;
		width: 80vw;
		padding-bottom: 30px;
	}

	.container {
		width: 100%;
		height: 100%;
		margin-bottom: 20px;
	}

	textarea {
		width: 100%;
		height: 70vh;
		line-height: 1.5em;
		white-space: nowrap;
	}

	p {
		word-wrap: break-word;
		line-height: 1.5em;
	}
</style>