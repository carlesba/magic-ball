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
		<div class="number-panel center scroll-animated front">8</div>
		<div class="back-panel center scroll-animated back">bla</div>
	</div>
</figure>

<style>
	:root {
		--size: 70vmin;
		--panel-size: 35vmin;
		background-color: #a0a0a0;
		--frame: 0;
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
		perspective-origin: center;
	}
	.panels > div {
		position: absolute;
		top: 0;
		left: 0;
	}
	@keyframes front {
		0% {
			opacity: 1;
		}
		29% {
			opacity: 1;
		}
		30% {
			opacity: 0;
		}
		100% {
			opacity: 0;
		}
	}
	@keyframes back {
		0% {
			opacity: 0;
		}
		29% {
			opacity: 0;
		}
		30% {
			opacity: 1;
		}
		100% {
			opacity: 1;
		}
	}
	.front {
		opacity: 1;
		animation-name: front;
		transform: translateZ(35vmin);
	}
	.back {
		animation-name: back;
		transform: translateZ(-35vmin) rotateX(180deg);
	}

	.number-panel {
		width: var(--panel-size);
		height: var(--panel-size);
		border-radius: 50%;
		background-color: white;
		color: black;
		font-family: sans-serif;
		font-size: var(--panel-size);
	}
	.back-panel {
		width: var(--panel-size);
		height: var(--panel-size);
		border-radius: 50%;
		background-color: white;
		color: black;
		font-family: sans-serif;
		font-size: var(--panel-size);
	}
</style>
