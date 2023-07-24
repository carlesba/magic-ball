<script lang="ts">
	let help = false;
	function toggleHelp(e: MouseEvent) {
		e.preventDefault();
		help = !help;
		document.documentElement.style.setProperty('--frame', '0');
	}
</script>

<header>
	<div class="menu">
		<a class="link-ball" href="/" aria-label="show help" on:click={toggleHelp}>?</a>
	</div>
</header>
<aside class="modal" class:visible={help}>
	<div class="menu">
		<a class="link-ball" href="/" on:click={toggleHelp} aria-label="close help">X</a>
	</div>
	<h1>Magic ball</h1>
	<article>
		<p>
			The magic ball can help you make decisions. Whenever you feel lost, ask the ball for advice.
		</p>
		<p>
			Just think of a question that can be answered with <i>Yes</i> or <i>No</i>. Concentrate very,
			very hard, and <i>scroll down to know the answer</i>.
		</p>
		<p>
			After reading the answer, explore <b>your feelings</b> and discover what your mind wants to tell
			you. If you're not confortable with the answer, maybe you should go for the opposite one. Sometimes,
			your feelings know more than your own reason.
		</p>
		<p>Scroll up to start over.</p>
		<hr />
		<p class="small">
			Done with Svelte by <a href="https://github.com/carlesba" aria-label="author" target="_blank"
				>Carles Ballester</a
			>
		</p>
	</article>
</aside>

<style>
	header {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		z-index: 1;
	}
	.menu {
		position: fixed;
		right: 1vmin;
		top: 1vmin;
		display: flex;
		align-items: center;
		justify-content: right;
	}
	hr {
		margin-top: 3em;
	}
	a {
		color: white;
	}
	.link-ball {
		text-decoration: none;
		display: inline-block;
		border-radius: 50%;
		width: 1.2em;
		line-height: 1.2em;
		height: 1.2em;
		text-align: center;

		text-shadow: 0 0.1vmin 0.1vmin rgba(0, 0, 0, 0.5);
		border: 2.5vmin solid #232323;
		color: black;
		font-size: 4vmin;
		background: white;
		font-family: sans-serif;
	}
	.modal {
		box-sizing: border-box;
		background: var(--bg);
		position: fixed;
		padding: 2vmin;
		height: 100vh;
		width: 100vw;
		top: 0;
		left: 0;
		opacity: 0;
		z-index: 1000;
		pointer-events: none;
		color: white;
		font-size: 40px;
		text-shadow: 2px 8px 10px rgba(0, 0, 0, 0.8);
		overflow-y: auto;
	}
	.modal h1 {
		text-align: center;
	}
	.modal p {
		max-width: 600px;
		margin: 1em auto;
	}
	.modal .small {
		font-size: 20px;
	}
	.modal.visible {
		opacity: 1;
		pointer-events: auto;
	}
</style>
