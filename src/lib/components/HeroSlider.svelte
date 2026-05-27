<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	import type { Swiper as SwiperType } from 'swiper';

	/* Slide data přenesená z originálu (Slider Revolution) */
	const slides = [
		{
			id: 'slide-www',
			bg: '/images/header32.jpg',
			bgPosition: '50% 50%',
			icon: '/images/www.png',
			iconAlt: 'WWW stránky',
			iconWidth: 82,
			textSide: 'left' as const,
			textDir: -1,   /* nálet zleva */
			small: 'JEDNODUCHÁ ADMINISTRACE',
			big: 'WWW STRÁNKY',
			sub: 'MODULÁRNÍ & RESPONZIVNÍ DESIGN',
		},
		{
			id: 'slide-marketing',
			bg: '/images/9.jpg',
			bgPosition: 'center top',
			icon: '/images/marketing.png',
			iconAlt: 'Online marketing',
			iconWidth: 75,
			textSide: 'right' as const,
			textDir: 1,    /* nálet zprava */
			small: 'S NÁMI SE NAHORU DOSTANETE',
			big: 'WEB MARKETING',
			sub: 'NÁVRATNOST INVESTIC',
		},
	];

	let swiperContainer: HTMLElement | undefined = $state();
	let swiperInstance: SwiperType | null = null;
	let activeIndex = $state(0);
	let textVisible = $state(false);

	function showText() {
		textVisible = false;
		setTimeout(() => { textVisible = true; }, 300);
	}

	onMount(async () => {
		const { Swiper } = await import('swiper');
		const { Pagination, Autoplay, EffectFade } = await import('swiper/modules');

		if (!swiperContainer) return;

		swiperInstance = new Swiper(swiperContainer, {
			modules: [Pagination, Autoplay, EffectFade],
			effect: 'fade',
			fadeEffect: { crossFade: true },
			loop: true,
			speed: 800,
			autoplay: {
				delay: 8400,
				disableOnInteraction: false,
			},
			pagination: {
				el: '.swiper-pagination',
				clickable: true,
			},
			on: {
				slideChange(s) {
					activeIndex = s.realIndex;
					showText();
				},
				init() {
					setTimeout(() => { textVisible = true; }, 100);
				},
			},
		});
	});

	onDestroy(() => {
		swiperInstance?.destroy();
	});
</script>

<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/swiper@12/swiper-bundle.min.css" />
</svelte:head>

<!--
	.hero-region je přímý potomek <body> (resp. mimo .wrapper),
	takže může být skutečně width: 100vw bez overflow clip.
-->
<div class="hero-region">
	<div class="swiper hero-swiper" bind:this={swiperContainer}>
		<div class="swiper-wrapper">
			{#each slides as slide, i (slide.id)}
				<div
					class="swiper-slide hero-slide"
					style="
						background-image: url('{slide.bg}');
						background-size: cover;
						background-position: {slide.bgPosition};
						background-repeat: no-repeat;
					"
				>
					<!--
						Vnitřní kontejner zachovává šířku 1200px vycentrovanou uvnitř
						full-width slidu — texty sedí na stejné pozici jako v originále.
					-->
					<div class="slide-inner">
						<div
							class="slide-text"
							class:pos-left={slide.textSide === 'left'}
							class:pos-right={slide.textSide === 'right'}
							class:visible={textVisible && activeIndex === i}
							style="--dir: {slide.textDir};"
						>
							<div class="slide-icon">
								<img src={slide.icon} alt={slide.iconAlt} width={slide.iconWidth} />
							</div>
							<p class="slide-small">{slide.small}</p>
							<p class="slide-big">{slide.big}</p>
							<p class="slide-sub">{slide.sub}</p>
						</div>
					</div>
				</div>
			{/each}
		</div>
		<div class="swiper-pagination"></div>
	</div>
</div>

<style>
	/* -------------------------------------------------------
	   Hero region — full viewport width, výška 500px
	------------------------------------------------------- */
	.hero-region {
		width: 100%;
		height: 500px;
		overflow: hidden;
		position: relative;
		background-color: #e9e9e9; /* fallback dokud se nenačte obrázek */
	}

	:global(.hero-swiper) {
		width: 100% !important;
		height: 500px !important;
	}

	:global(.hero-slide) {
		width: 100% !important;
		height: 500px !important;
		position: relative;
	}

	/* -------------------------------------------------------
	   Centrovaný kontejner uvnitř slidu (1200px jako wrapper)
	   — text sedí na stejných x/y pozicích jako v originále
	------------------------------------------------------- */
	.slide-inner {
		width: 100%;
		max-width: 1200px;
		height: 100%;
		margin: 0 auto;
		position: relative;
	}

	/* -------------------------------------------------------
	   Slide-text blok — absolutní uvnitř slide-inner
	------------------------------------------------------- */
	.slide-text {
		position: absolute;
		display: flex;
		flex-direction: column;
		top: 100px;           /* yo originálu: ikon ~182px, small ~279px od vrchu */
	}

	/* Slide 1: text vlevo (xo: 10px od levého okraje) */
	.slide-text.pos-left {
		left: 43px;
	}

	/* Slide 2: text vpravo (xo: 460px = 38 % z 1200px) */
	.slide-text.pos-right {
		left: 38.3%;  /* ≈ 460 / 1200 */
	}

	/* -------------------------------------------------------
	   Ikona — vždy letí zleva (originál: data-frame_0="x:-50px")
	------------------------------------------------------- */
	.slide-icon {
		opacity: 0;
		transform: translateX(-50px);
		transition: opacity 0.6s cubic-bezier(0.19, 1, 0.22, 1) 0.9s,
					transform 0.6s cubic-bezier(0.19, 1, 0.22, 1) 0.9s;
		margin-bottom: 10px;
	}

	/* -------------------------------------------------------
	   Texty — směr náletu řízen --dir (-1 = zleva, 1 = zprava)
	------------------------------------------------------- */
	.slide-small,
	.slide-big,
	.slide-sub {
		opacity: 0;
		transform: translateX(calc(var(--dir, 1) * 120px));
		margin: 0;
		white-space: nowrap;
	}

	.slide-small {
		transition: opacity 0.5s cubic-bezier(0.19, 1, 0.22, 1) 0.3s,
					transform 0.5s cubic-bezier(0.19, 1, 0.22, 1) 0.3s;
		font-family: 'Oswald', sans-serif;
		font-size: 20px;
		font-weight: 500;
		color: #262626;
		line-height: 36px;
		letter-spacing: 0;
	}

	.slide-big {
		transition: opacity 0.8s cubic-bezier(0.19, 1, 0.22, 1) 0.5s,
					transform 0.8s cubic-bezier(0.19, 1, 0.22, 1) 0.5s;
		font-family: 'Oswald', sans-serif;
		font-size: 100px;
		font-weight: 500;
		color: #e91b23;
		line-height: 1;
		letter-spacing: 1px;
	}

	.slide-sub {
		transition: opacity 0.9s cubic-bezier(0.19, 1, 0.22, 1) 0.7s,
					transform 0.9s cubic-bezier(0.19, 1, 0.22, 1) 0.7s;
		font-family: 'Oswald', sans-serif;
		font-size: 50px;
		font-weight: 500;
		color: #262626;
		line-height: 36px;
	}

	/* Visible stav — vše animuje na místo */
	.slide-text.visible .slide-icon,
	.slide-text.visible .slide-small,
	.slide-text.visible .slide-big,
	.slide-text.visible .slide-sub {
		opacity: 1;
		transform: translateX(0);
	}

	/* -------------------------------------------------------
	   Swiper pagination
	------------------------------------------------------- */
	:global(.hero-region .swiper-pagination) {
		bottom: 15px;
	}

	:global(.hero-region .swiper-pagination-bullet) {
		background: rgba(0, 0, 0, 0.5);
		opacity: 1;
	}

	:global(.hero-region .swiper-pagination-bullet-active) {
		background: #e91b23;
	}

	/* -------------------------------------------------------
	   Responsive
	------------------------------------------------------- */
	@media screen and (max-width: 1200px) {
		.slide-text.pos-right { left: 40%; }
	}

	@media screen and (max-width: 1024px) {
		.hero-region,
		:global(.hero-swiper),
		:global(.hero-slide) { height: 400px; }

		:global(.hero-swiper) { height: 400px !important; }
		:global(.hero-slide)  { height: 400px !important; }

		.slide-big { font-size: 70px; }
		.slide-sub { font-size: 35px; }
	}

	@media screen and (max-width: 768px) {
		.hero-region,
		:global(.hero-swiper),
		:global(.hero-slide) { height: 440px; }

		:global(.hero-swiper) { height: 440px !important; }
		:global(.hero-slide)  { height: 440px !important; }

		.slide-text.pos-left,
		.slide-text.pos-right {
			left: 10px;
			top: 80px;
		}

		.slide-big { font-size: 45px; white-space: normal; }
		.slide-sub { font-size: 35px; white-space: normal; line-height: 40px; }
		.slide-small { font-size: 16px; }
	}
</style>
