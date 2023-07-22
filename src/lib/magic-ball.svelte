<script lang="ts">
	function onScroll() {
		const { scrollTop, scrollHeight, clientHeight } = document.documentElement;
		const maxScrollTop = scrollHeight - clientHeight;
		const percent = scrollTop / maxScrollTop;
		document.documentElement.style.setProperty('--frame', percent.toString());
	}
</script>

<svelte:window on:scroll={onScroll} />

<figure class="ball center">
	<div class="panels scroll-animated">
		<div class="number-panel center scroll-animated">8</div>
		<div class="back-panel center scroll-animated">bla</div>
	</div>
</figure>

<style>
	:root {
		--size: 70vmin;
		--panel-size: 35vmin;
		background-color: #a0a0a0;
		--frame: 0.5;
	}

	.scroll-animated {
		/* Pause the animation */
		animation-play-state: paused;
		/* Bind the animation to scroll */
		animation-delay: calc(var(--frame) * -1s);
		/* These last 2 properites clean up overshoot weirdness */
		animation-iteration-count: 1;
		animation-fill-mode: both;
		animation-duration: 1s;
	}

	.center {
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.ball {
		width: var(--size);
		aspect-ratio: 1;
		background-color: black;
		box-shadow: inset -1vmin 0vmin 4vmin rgba(255, 255, 255, 0.2), 0 4vmin 8vmin rgba(0, 0, 0, 0.5);
		background-image: linear-gradient(-45deg, rgba(255, 255, 220, 0.3) 0%, transparent 100%);

		border-radius: 50%;
		overflow: hidden;
	}

	@keyframes ball-flip {
		from {
			transform: rotateX(0deg);
		}
		to {
			transform: rotateX(180deg);
		}
	}
	.panels {
		width: var(--panel-size);
		height: var(--panel-size);
		transform-style: preserve-3d;
		animation-name: ball-flip;
		transform: rotateX(0deg);
		animation-timing-function: linear;
		transform-style: preserve-3d;
		perspective-origin: center;
	}
	.panels > div {
		position: absolute;
	}

	@keyframes front {
		0% {
			visibility: hidden;
		}
		50% {
			visibility: hidden;
		}
	}

	.number-panel {
		transform: translateZ(35vmin);
		width: var(--panel-size);
		height: var(--panel-size);
		border-radius: 50%;
		background-color: white;
		color: black;
		font-family: sans-serif;
		font-size: var(--panel-size);
		animation: front;
	}
	.back-panel {
	visibility: hidden;
		transform: translateZ(-35vmin) rotateX(180deg);
		width: var(--panel-size);
		height: var(--panel-size);
		border-radius: 50%;
		background-color: white;
		color: black;
		font-family: sans-serif;
		font-size: var(--panel-size);
	}
</style>
