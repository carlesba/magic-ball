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
	<span class="shadow" />
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
		position: relative;
		background: radial-gradient(circle at 50% 120%, #323232, #0a0a0a 80%, #000000 100%);
		width: var(--size);
		aspect-ratio: 1;
		box-shadow: inset -1vmin 0vmin 4vmin rgba(255, 255, 255, 0.2), 0 4vmin 8vmin rgba(0, 0, 0, 0.8);

		border-radius: 50%;
		overflow: hidden;
	}
	.ball:before {
		content: '';
		position: absolute;
		background: radial-gradient(
			circle at 50% 120%,
			rgba(255, 255, 255, 0.5),
			rgba(255, 255, 255, 0) 70%
		);
		border-radius: 50%;
		bottom: 2.5%;
		left: 5%;
		opacity: 0.3;
		height: 100%;
		width: 90%;
		filter: blur(2vmin);
		z-index: 2;
	}
	.ball:after {
		width: 100%;
		height: 100%;
		content: '';
		position: absolute;
		top: 5%;
		left: 10%;
		border-radius: 50%;
		background: radial-gradient(
			circle at 50% 50%,
			rgba(255, 255, 255, 0.8),
			rgba(255, 255, 255, 0.8) 14%,
			rgba(255, 255, 255, 0) 24%
		);
		opacity: 0.5;
		transform: translateX(-20vmin) translateY(-24vmin) skewX(-20deg);
		filter: blur(4vmin);
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
	.shadow {
		position: absolute;
		top: 0;
		left: 0;
		width: var(--size);
		height: var(--size);
		background: radial-gradient(
			circle at 50% 50%,
			rgba(0, 0, 0, 0.4),
			rgba(0, 0, 0, 0.1) 40%,
			rgba(0, 0, 0, 0) 50%
		);
	}
</style>
