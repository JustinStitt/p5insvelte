<script>
	/*
		npm install --save svelte svelte-loader (webpack)
		npm install p5-svelte
		npm install -D p5 

		npx degit sveltejs/template-webpack svelte-app
		cd svelte-app
	*/
	import P5 from 'p5-svelte';

	let y = 100;
	let width = 400;
	let height = 400;
	const sketch = (p5) => {
		p5.setup = () => {
			p5.createCanvas(width, height);
			p5.frameRate(60);
		}; // end setup

		p5.draw = () => {
			p5.background(255, 0, 0)
			p5.ellipse(100, y, 20, 20);
			y -= 1 * p5.deltaTime / 10;
		}; // end draw

		p5.mousePressed = () => {
			if (!mouseInCanvas({x: p5.mouseX, y: p5.mouseY})) return;
			moveY();
		}
	}; // end sketch

	const mouseInCanvas = (mpos) => {
		if (mpos.x < 0 || mpos.x > width) return false;
		if (mpos.y < 0 || mpos.y > height) return false;
		return true;
	}

	const moveY = () => {
		y = 100;
	};

</script>

<main>
	<h1>P5 in Svelte!</h1>
	<div class="canvas">
		<P5 {sketch}/>
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: .5em;
		max-width: 240px;
		margin: 0 auto;

		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		background-color: coral;
	}

	h1 {
		font-size: 2em;
		font-weight: 500;
		margin: 0;
	}

	.canvas {
		background-color: lightblue;
		padding: 3px 3px 0 3px;
	}

</style>
