<script lang="ts">
	const maxPointsPerStat = 100;
	const stats: { icon: string; name: string; color: string; result: number }[] = [
		{ icon: 'icon-reaction', name: 'Reaction', color: 'light-red', result: randomNum() },
		{ icon: 'icon-memory', name: 'Memory', color: 'orangey-yellow', result: randomNum() },
		{ icon: 'icon-verbal', name: 'Verbal', color: 'green-teal', result: randomNum() },
		{ icon: 'icon-visual', name: 'Visual', color: 'cobalt-blue', result: randomNum() }
	];
	const fullScore = calculateFullScore();
	const scoreName = nameTheScore(fullScore);
	const betterThanHowMany = randomNum();

	function randomNum() {
		return Math.floor(Math.random() * (maxPointsPerStat + 1));
	}

	function calculateFullScore() {
		const pointsSum = stats.reduce((prev, curr) => prev + curr.result, 0);
		const maxPoints = stats.length * maxPointsPerStat;
		return Math.floor((pointsSum * 100) / maxPoints);
	}

	function nameTheScore(score: number) {
		if (score < 20) {
			return 'Insufficient';
		} else if (score < 40) {
			return 'Allowing';
		} else if (score < 60) {
			return 'Sufficient';
		} else if (score < 80) {
			return 'Good';
		} else {
			return 'Great';
		}
	}
</script>

<section class="summary-section-container">
	<section class="score-section">
		<h3>Your Result</h3>
		<div class="points">
			<span class="gained">{fullScore}</span>
			<span class="max">of {maxPointsPerStat}</span>
		</div>
		<div class="description">
			<h2>{scoreName}</h2>
			<p>
				You scored higher then {betterThanHowMany}% of the people who have taken these tests;
			</p>
		</div>
	</section>
	<section class="stat-section">
		<h3>Summary</h3>
		<ul class="stat-list">
			{#each stats as stat}
				<li class="stat-row {stat.color}">
					<div class="flex">
						<img src={`/icons/${stat.icon}.svg`} alt={`Icon for statistic ${stat.name}`} />
						<span class="stat-name">{stat.name}</span>
					</div>
					<b class="stat-result">{stat.result} / {maxPointsPerStat}</b>
				</li>
			{/each}
		</ul>
		<button>Continue</button>
	</section>
</section>

<style lang="scss">
	$section-padding: 2em;
	$gradient-light-slate-blue: hsl(252, 100%, 67%);
	$gradient-light-royal-blue: hsl(241, 81%, 54%);
	$gradient-violet-blue: hsla(256, 72%, 46%, 1);
	$gradient-persian-blue: hsla(241, 72%, 46%, 0);
	$color-light-red: hsl(0, 100%, 67%);
	$background-light-red: hsla(0, 100%, 67%, 0.2);
	$color-orangey-yellow: hsl(39, 100%, 56%);
	$background-orangey-yellow: hsla(39, 100%, 56%, 0.2);
	$color-green-teal: hsl(166, 100%, 37%);
	$background-green-teal: hsla(166, 100%, 37%, 0.2);
	$color-cobalt-blue: hsl(234, 85%, 45%);
	$background-cobalt-blue: hsla(234, 85%, 45%, 0.2);
	$color-white: hsl(0, 0%, 100%);
	$color-pale-blue: hsl(221, 100%, 96%);
	$color-light-lavender: hsl(241, 100%, 89%);
	$color-dark-blue: hsl(224, 30%, 27%);

	:root {
		font-size: 18px;
		font-family: 'HankenGrotesk-Medium', sans-serif;
	}

	.light-red {
		color: $color-light-red;
		background: $background-light-red;
	}
	.orangey-yellow {
		color: $color-orangey-yellow;
		background: $background-orangey-yellow;
	}
	.green-teal {
		color: $color-green-teal;
		background: $background-green-teal;
	}
	.cobalt-blue {
		color: $color-cobalt-blue;
		background: $background-cobalt-blue;
	}

	section.summary-section-container {
		display: flex;
		background: #fff;
		-webkit-box-shadow: 2px 2px 6px -1px rgba(66, 68, 90, 1);
		-moz-box-shadow: 2px 2px 6px -1px rgba(66, 68, 90, 1);
		box-shadow: 2px 2px 6px -1px rgba(66, 68, 90, 1);
		border-radius: 2em;
		max-width: 40em;
		margin: 0 auto;
	}

	h2 {
		font-size: 2em;
		font-family: 'HankenGrotesk-ExtraBold';
	}

	h3 {
		font-size: 1.4em;
		font-family: 'HankenGrotesk-Bold';
	}

	.score-section {
		flex: 1;
		border-radius: 2em;
		background: linear-gradient($gradient-light-slate-blue, $gradient-light-royal-blue);
		padding: $section-padding;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-direction: column;

		& > h3 {
			color: $color-light-lavender;
		}

		h2,
		h3 {
			text-align: center;
		}

		.points {
			border-radius: 100%;
			width: 9em;
			aspect-ratio: 1;
			display: flex;
			align-items: center;
			justify-content: center;
			flex-direction: column;
			background: linear-gradient($gradient-violet-blue, $gradient-persian-blue);

			.gained {
				color: $color-pale-blue;
				font-size: 3em;
				font-family: 'HankenGrotesk-ExtraBold';
			}

			.max {
				color: $gradient-light-slate-blue;
			}
		}

		.description {
			padding: 0 1em;
			text-align: center;
			h2 {
				color: $color-white;
			}
			p {
				color: $color-light-lavender;
			}
		}
	}

	.stat-section {
		flex: 1;
		padding: $section-padding;
		display: flex;
		flex-direction: column;
		justify-content: space-between;

		h3 {
			color: $color-dark-blue;
			margin-bottom: 0;
		}

		ul.stat-list {
			list-style: none;
			display: flex;
			flex-direction: column;
			gap: 0.5em;
			padding: 0;
			margin: 0;

			li.stat-row {
				border-radius: 1em;
				padding: 1em;
				display: flex;
				align-items: center;
				justify-content: space-between;

				img {
					margin-right: 1em;
				}
				.stat-result {
				}
			}
		}

		button {
			width: 100%;
			text-align: center;
			padding: 0.5em;
			border-radius: 1em;
			border: none;
			font-family: 'HankenGrotesk-Bold';
			color: $color-white;
			background: linear-gradient($gradient-light-slate-blue, $gradient-light-royal-blue);
			cursor: pointer;

			&:active {
				background: $color-dark-blue;
			}
		}
	}

	@media screen and (max-width: 700px) {
		section.summary-section-container {
			width: 100%;
			max-width: unset;
			flex-direction: column;
			border-radius: 0 0 2em 2em;
		}

		.score-section {
			border-radius: 0 0 2em 2em;
		}

		.stat-section {
			gap: 1em;

			h3 {
				margin: 0;
			}
		}
	}
</style>
