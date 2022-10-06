<div class="left">
	<h1>Spotifds</h1>
	<div class="menuSelector">
		<a href="/">Main Page</a>
		<a href="/manage">Manage</a>
	</div>
</div>

<style>
	.left {
		background-color: var(--primary-background-color);
		grid-area: panel;
		padding: 25px 25px;
		box-shadow: 0px 0px 5px black;
	}
	h1 {
		text-align: center;
		margin-bottom: 50px;
		color: var(--lighting-pink);
		text-shadow: var(--title-light);
		animation: flicker 8s infinite;

		--title-light-less: 0 0 3px var(--lighting-pink), 0 0 5px var(--lighting-pink), 0 0 8px var(--lighting-pink), 0 0 16px var(--pink),
			0 0 18px var(--pink), 0 0 30px var(--pink), 0 0 34px var(--pink),
			0 0 40px var(--pink);
		--title-light-hight: 0 0 3px var(--lighting-pink-on), 0 0 6px var(--lighting-pink-on), 0 0 10px var(--lighting-pink-on), 0 0 18px var(--pink),
			0 0 30px var(--pink), 0 0 34px var(--pink), 0 0 40px var(--pink),
			0 0 45px var(--pink);
	}

	@keyframes flicker {
		/* 0%,
		75%,
		100% {
			color: var(--lighting-pink);
			text-shadow: var(--title-light-less);
		}

		50% {
			color: var(--lighting-pink-on);
			text-shadow: var(--title-light-hight);
		} */
		/* pq ele ta pulsando 2 vezes aaaah */
		0%,
		100% {
			color: var(--lighting-pink);
			text-shadow: var(--title-light-less);
		}

		50% {
			color: #fff;
			text-shadow: var(--title-light-hight);
		}
	}

	.menuSelector {
		width: 100%;
		display: flex;
		flex-direction: column;
		margin-left: 10px;
	}

	.menuSelector a {
		text-decoration: none;
		font-size: 22px;
		color: #ffffff;
		transition: 0.3s;
		padding-bottom: 10px;
	}

	.menuSelector a:hover {
		transition: 0.3s;
		margin-left: 10px;
	}

	.menuSelector a:active {
		color: var(--yellow);
		position: relative;
		top: 2px;
		transition: 0s;
		text-shadow: 0 0 3px var(--yellow), 0 0 5px var(--yellow), 0 0 8px var(--yellow),
			0 0 18px var(--orange), 0 0 30px var(--orange), 0 0 34px var(--orange),
			0 0 40px var(--orange), 0 0 65px var(--orange);
	}
</style>
