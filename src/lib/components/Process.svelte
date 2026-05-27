<script lang="ts">
	import { onMount } from 'svelte';

	const steps = [
		{
			id: 'cile',
			num: '01',
			numSize: '100px',
			img: '/images/parallax-1.png',
			title: 'URČENÍ CÍLŮ, STRATEGIE',
			text: 'Specifikujeme si vše co je potřeba pro realizaci Vašeho projektu včetně krátkodobých i dlouhodobých cílů.',
			delay: 500,
		},
		{
			id: 'realizace',
			num: '02',
			numSize: '100px',
			img: '/images/home1.png',
			title: 'PRECIZNÍ REALIZACE',
			text: 'Každému kroku věnujeme maximum péče a průběžně s Vámi konzultujeme veškeré náležitosti až do finální podoby.',
			delay: 1000,
		},
		{
			id: 'analytika',
			num: '03',
			numSize: '95px',
			img: '/images/image1.png',
			title: 'ANALYTIKA, OPTIMALIZACE',
			text: 'Vždy se klientům snažíme poskytnout komplexní péči a veškeré kroky online marketingu založit na přesné analytice.',
			delay: 1500,
		},
	];

	/* Flip stav pro každou kartu — true = otočená (back viditelný) */
	let flipped = $state([false, false, false]);
	/* Animace vstupu do viewportu */
	let appeared = $state([false, false, false]);
	let sectionEl: HTMLElement | undefined = $state();

	onMount(() => {
		if (!sectionEl) return;

		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						steps.forEach((step, i) => {
							setTimeout(() => {
								appeared[i] = true;
								appeared = [...appeared];
							}, step.delay - 500);
						});
						observer.disconnect();
					}
				});
			},
			{ threshold: 0.2 }
		);

		observer.observe(sectionEl);
		return () => observer.disconnect();
	});
</script>

<section class="content_section process-section" id="proces" bind:this={sectionEl}>
	<div class="section-wrap">
	<h2>PROCES REALIZACE</h2>
	<div class="separator transparent" style="margin: 14px 0 10px;"></div>

	<div class="three_columns clearfix">
		{#each steps as step, i (step.id)}
			<div class="column1">
				<div class="column_inner">

					<!-- Flip karta -->
					<!-- svelte-ignore a11y_no_static_element_interactions -->
					<div
						class="flip-card"
						class:appeared={appeared[i]}
						class:flipped={flipped[i]}
						onmouseenter={() => { flipped[i] = true; flipped = [...flipped]; }}
						onmouseleave={() => { flipped[i] = false; flipped = [...flipped]; }}
					>
						<div class="flip-card-inner">
							<!-- Přední strana (obrázek) -->
							<div class="flip-front">
								<img src={step.img} alt={step.title} loading="lazy" />
							</div>
							<!-- Zadní strana (červené pozadí + text) -->
							<div class="flip-back">
								<div class="flip-back-text">
									<h4>{step.title}</h4>
								</div>
							</div>
						</div>
					</div>

					<div class="separator transparent" style="margin: 20px 0 10px;"></div>

					<!-- Číslo + popis (2 sloupce 33/66) -->
					<div class="two_columns_33_66 clearfix">
						<div class="col-num">
							<span
								class="step-num"
								style="font-size: {step.numSize}; line-height: {step.numSize};"
							>{step.num}</span>
						</div>
						<div class="col-text">
							<h4>{step.title}</h4>
							<p>{step.text}</p>
						</div>
					</div>

				</div>
			</div>
		{/each}
	</div>
	</div>
</section>

<style>
	section.process-section {
		background-color: #f1f1f1;
		padding: 80px 0;
	}

	.three_columns > .column1 {
		width: 33.33%;
		float: left;
	}

	.column_inner {
		padding: 0 20px;
	}

	h2 {
		font-family: 'Oswald', sans-serif;
		font-size: 40px;
		line-height: 40px;
		font-weight: 500;
		color: #262626;
		margin: 0 0 20px;
	}

	/* -------------------------------------------------------
	   Flip karta (z originálu: flip_image_holder / flip_image)
	------------------------------------------------------- */
	.flip-card {
		position: relative;
		cursor: pointer;
		width: 100%;
		/* poměr originálu: obrázky jsou přibližně čtvercové */
		aspect-ratio: 1 / 0.75;
		perspective: 600px;
		opacity: 0;
		transform: translateY(20px);
		transition: opacity 0.5s ease, transform 0.5s ease;
	}

	.flip-card.appeared {
		opacity: 1;
		transform: translateY(0);
	}

	.flip-card-inner {
		position: relative;
		width: 100%;
		height: 100%;
		transform-style: preserve-3d;
		transition: transform 0.6s cubic-bezier(0.4, 0, 0.2, 1);
	}

	.flip-card.flipped .flip-card-inner {
		transform: rotateY(180deg);
	}

	/* Přední a zadní strana */
	.flip-front,
	.flip-back {
		position: absolute;
		inset: 0;
		backface-visibility: hidden;
		-webkit-backface-visibility: hidden;
	}

	.flip-front img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		display: block;
	}

	.flip-back {
		background-color: #3c8eba;
		transform: rotateY(180deg);
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.flip-back-text {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;
		height: 100%;
	}

	.flip-back-text h4 {
		font-family: 'Oswald', sans-serif;
		font-size: 20px;
		line-height: 20px;
		font-weight: 500;
		color: #fff;
		text-align: center;
		margin: 0;
		padding: 20px;
	}

	/* -------------------------------------------------------
	   Číslo + popis (2 sloupce)
	------------------------------------------------------- */
	.two_columns_33_66 {
		width: 100%;
	}

	.col-num {
		width: 33.33%;
		float: left;
	}

	.col-text {
		width: 66.66%;
		float: left;
		padding-left: 10px;
	}

	.step-num {
		font-family: 'Oswald', sans-serif;
		font-weight: 400;
		color: #262626;
		display: block;
		line-height: 1;
	}

	h4 {
		font-family: 'Oswald', sans-serif;
		font-size: 20px;
		line-height: 20px;
		font-weight: 500;
		color: #262626;
		margin: 0 0 10px;
	}

	p {
		font-family: 'PT Sans', sans-serif;
		font-size: 13px;
		line-height: 22px;
		color: #4f4f4f;
		margin: 0;
	}

	/* -------------------------------------------------------
	   Responsive
	------------------------------------------------------- */
	@media screen and (max-width: 1024px) {
		.three_columns > .column1 {
			width: 100%;
			float: none;
			margin-bottom: 40px;
		}
	}

	@media screen and (max-width: 768px) {
		.step-num { font-size: 60px !important; line-height: 60px !important; }
	}
</style>
