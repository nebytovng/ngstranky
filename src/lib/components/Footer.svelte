<script lang="ts">
	const NG = 'https://www.ngstranky.cz';

	const posts = [
		{
			id: 'email-klient',
			day: '05',
			month: 'Feb',
			title: 'Propojení e-mailové schránky s e-mailovým klientem',
			excerpt: 'Chcete-li využívat nástroj na správu e-mailové schránky, je třeba nastavit adresy a porty ve vašem e-mailovém klientovi.',
			path: '/propojeni-emailove-schranky-s-emailovym-klientem/',
		},
		{
			id: 'axa',
			day: '05',
			month: 'Oct',
			title: 'Spolupracujeme s AXA Assistance na rozvoji online kanálů napříč Evropou',
			excerpt: 'Od roku 2024 jsme navázali novou spolupráci se společností AXA Assistance, jednou z předních pojišťovacích skupin v Evropě.',
			path: '/zjednodusujeme-online-cestu-klientum-axa-assistance/',
		},
	];

	const references = [
		{ img: '/images/autoskola-havlik-nahled.jpg', alt: 'Autoškola Havlík', path: '/portfolio_page/autoskola-havlik-2/' },
		{ img: '/images/pizza-free-nahled.jpg',        alt: 'Pizza Free',        path: '/portfolio_page/pizza-free/' },
		{ img: '/images/aterion-nahled.jpg',           alt: 'Aterion',           path: '/portfolio_page/aterion/' },
		{ img: '/images/alupress-nahled.jpg',          alt: 'Alupress',          path: '/portfolio_page/4667/' },
	];
</script>

<footer>
	<div class="footer-top">
		<div class="section-wrap">
			<div class="four_columns clearfix">

				<!-- Sloupec 1: Kontaktní informace -->
				<div class="column1">
					<div class="column_inner">
						<h4>Kontaktní informace</h4>
						<img src="/images/ng-logo-bez-mezer.png" alt="NG Consulting" class="footer-logo" />
						<p>NG Consulting s.r.o.<br />
						Hanychovská 575/33,<br />
						460 07 Liberec</p>
						<p>
							Email: <a href="mailto:info@ngstranky.cz?subject=Dotaz%20z%20webu">info@ngstranky.cz</a><br />
							Tel.: <a href="tel:00420775133557">+420 775 133 557</a><br />
							Tel.: <a href="tel:00420608133557">+420 608 133 557</a>
						</p>
						<p>Sociální sítě:
							<span class="ngsoc">
								<a href="https://www.facebook.com/ngstranky/" target="_blank" rel="nofollow noopener noreferrer" aria-label="Facebook">
									<i class="fa fa-facebook" aria-hidden="true"></i>
								</a>
								<a href="https://twitter.com/ngstranky" target="_blank" rel="nofollow noopener noreferrer" aria-label="Twitter">
									<i class="fa fa-twitter" aria-hidden="true"></i>
								</a>
								<a href="https://cz.linkedin.com/company/ng-consulting-s-r-o-" target="_blank" rel="nofollow noopener noreferrer" aria-label="LinkedIn">
									<i class="fa fa-linkedin" aria-hidden="true"></i>
								</a>
							</span>
						</p>
					</div>
				</div>

				<!-- Sloupec 2: Ohlasy klientů -->
				<div class="column2">
					<div class="column_inner">
						<h4>Ohlasy našich klientů</h4>
						<div class="review-box">
							<div class="review-stars" aria-label="5 hvězdiček">★★★★★</div>
							<div class="review-text">
								Jménem on-line šachové herny a e-shopu Šachy.cz bych rád vyjádřil své poděkování
								ing. Jakubu Vytiskovi a službě ngstranky.cz. Díky jejich službám a profesionální
								pomoci se nám podařilo nastartovat projekt šachy.cz. Komunikace byla vždy rychlá
								a korektní, ale zároveň vřelá a osobní. Vše šlo řešit s individuálním přístupem.
							</div>
							<div class="review-author">
								Jan Jílek —
								<a href="https://sachy.cz/" target="_blank" rel="nofollow noopener noreferrer">sachy.cz</a>
							</div>
						</div>
					</div>
				</div>

				<!-- Sloupec 3: Aktuality -->
				<div class="column3">
					<div class="column_inner">
						<h4>Aktuality</h4>
						<div class="latest_post_small_holder clearfix">
							{#each posts as post (post.id)}
								<div class="latest_post_small">
									<div class="date_holder">
										<span class="day">{post.day}</span>
										<span class="month">{post.month}</span>
									</div>
									<div class="content_holder">
										<h4><a href={NG + post.path} target="_blank" rel="noopener noreferrer">{post.title}</a></h4>
										<p>{post.excerpt}</p>
									</div>
								</div>
							{/each}
						</div>
					</div>
				</div>

				<!-- Sloupec 4: Vybrané reference -->
				<div class="column4">
					<div class="column_inner">
						<h4>Vybrané reference</h4>
						<div class="ref-grid">
							{#each references as ref (ref.img)}
								<a href={NG + ref.path} target="_blank" rel="noopener noreferrer">
									<img src={ref.img} alt={ref.alt} loading="lazy" />
								</a>
							{/each}
						</div>
					</div>
				</div>

			</div>
		</div>
	</div>

	<div class="footer-bottom">
		<div class="section-wrap">
			<p>
				Created by ngstránky.cz 2026. All rights Reserved. |
				<a
					href="https://www.ngstranky.cz/wp-content/uploads/2018/04/ochrana-osobn%C3%ADch-%C3%BAdaj%C5%AF.pdf"
					target="_blank"
					rel="noopener noreferrer"
				>ochrana osobních údajů</a>
			</p>
		</div>
	</div>
</footer>

<style>
	/* -------------------------------------------------------
	   Footer wrapper
	------------------------------------------------------- */
	footer {
		background-color: #262626;
		display: block;
		width: 100%;
		position: relative;
	}

	/* -------------------------------------------------------
	   Footer top
	------------------------------------------------------- */
	.footer-top {
		padding: 55px 0 25px;
	}

	/* Sloupce — šířky přesně podle originálu */
	.four_columns > .column1,
	.four_columns > .column2,
	.four_columns > .column3,
	.four_columns > .column4 {
		width: 25%;
		float: left;
	}

	/* Asymetrické odsazení */
	.four_columns > .column1 > .column_inner { padding: 0 16px 0 0; }
	.four_columns > .column2 > .column_inner { padding: 0 10px 0 6px; }
	.four_columns > .column3 > .column_inner { padding: 0 6px 0 10px; }
	.four_columns > .column4 > .column_inner { padding: 0 0 0 16px; }

	/* Typografie — orig: .footer_top a, p, span = #a0a0a0; h4 = #fff */
	h4 {
		font-family: 'Oswald', sans-serif;
		font-size: 20px;
		line-height: 20px;
		font-weight: 500;
		color: #fff;
		margin: 0 0 23px;
	}

	p {
		font-family: 'PT Sans', sans-serif;
		font-size: 13px;
		line-height: 22px;
		color: #a0a0a0;
		margin: 10px 0;
	}

	a {
		color: #a0a0a0;
		text-decoration: none;
	}

	a:hover {
		color: #fff;
	}

	/* -------------------------------------------------------
	   Sloupec 1: logo + sociální sítě
	------------------------------------------------------- */
	.footer-logo {
		display: block;
		margin: 0 0 10px;
		max-width: 100%;
	}

	.ngsoc a {
		padding: 0 5px;
		color: #a0a0a0;
	}

	.ngsoc a:hover {
		color: #fff;
	}

	/* -------------------------------------------------------
	   Sloupec 2: hodnocení
	------------------------------------------------------- */
	.review-box {
		background-color: #333;
		padding: 14px;
	}

	.review-stars {
		color: #f5a623;
		font-size: 16px;
		letter-spacing: 2px;
		margin-bottom: 8px;
	}

	.review-text {
		font-family: 'PT Sans', sans-serif;
		font-size: 12px;
		line-height: 20px;
		color: #a0a0a0;
		margin-bottom: 10px;
	}

	.review-author {
		font-family: 'PT Sans', sans-serif;
		font-size: 12px;
		font-weight: 700;
		color: #a0a0a0;
	}

	.review-author a {
		color: #a0a0a0;
	}

	.review-author a:hover {
		color: #fff;
	}

	/* -------------------------------------------------------
	   Sloupec 3: aktuality — přesně podle originálu
	------------------------------------------------------- */
	.latest_post_small {
		display: inline-block;
		width: 100%;
		padding: 0 0 20px;
		margin: 0 0 20px;
		border-bottom: 1px solid #666;
		min-height: 60px;
		box-sizing: border-box;
	}

	.latest_post_small:last-child {
		border-bottom: none;
		margin-bottom: 0;
	}

	.date_holder {
		width: 60px;
		height: 60px;
		background-color: #333;
		float: left;
	}

	.date_holder .day {
		font-family: 'Oswald', sans-serif;
		font-size: 25px;
		line-height: 25px;
		color: #fff;
		display: block;
		text-align: center;
		margin: 10px 0 0;
	}

	.date_holder .month {
		font-family: 'Oswald', sans-serif;
		font-size: 12px;
		line-height: 12px;
		color: #fff;
		display: block;
		text-align: center;
		text-transform: uppercase;
		margin: 5px 0 0;
	}

	.content_holder {
		padding: 0 0 0 80px;
	}

	.content_holder h4 {
		font-family: 'Oswald', sans-serif;
		font-size: 14px;
		line-height: 14px;
		margin: 0;
		color: #a0a0a0;
		text-transform: uppercase;
	}

	.content_holder h4 a {
		color: #a0a0a0;
	}

	.content_holder h4 a:hover {
		color: #fff;
	}

	.content_holder p {
		color: #fff;
		margin: 10px 0 0;
		font-size: 12px;
		line-height: 18px;
	}

	/* -------------------------------------------------------
	   Sloupec 4: reference grid 2×2
	------------------------------------------------------- */
	.ref-grid {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 4px;
	}

	.ref-grid a {
		display: block;
		overflow: hidden;
	}

	.ref-grid img {
		width: 100%;
		height: auto;
		display: block;
		transition: opacity 0.3s ease;
	}

	.ref-grid a:hover img {
		opacity: 0.8;
	}

	/* -------------------------------------------------------
	   Footer bottom — černý pruh
	------------------------------------------------------- */
	.footer-bottom {
		background-color: #000;
		height: 50px;
		line-height: 50px;
	}

	.footer-bottom .section-wrap {
		height: 100%;
	}

	.footer-bottom p {
		font-family: 'Oswald', sans-serif;
		font-size: 14px;
		color: #a0a0a0;
		margin: 0;
		text-align: center;
		line-height: 50px;
	}

	.footer-bottom a {
		color: #a0a0a0;
	}

	.footer-bottom a:hover {
		color: #fff;
	}

	/* -------------------------------------------------------
	   Responsive
	------------------------------------------------------- */
	@media screen and (max-width: 1024px) {
		.four_columns > .column1,
		.four_columns > .column2,
		.four_columns > .column3,
		.four_columns > .column4 {
			width: 50%;
		}

		.four_columns > .column1 > .column_inner,
		.four_columns > .column2 > .column_inner,
		.four_columns > .column3 > .column_inner,
		.four_columns > .column4 > .column_inner {
			padding: 0 10px;
		}
	}

	@media screen and (max-width: 768px) {
		.four_columns > .column1,
		.four_columns > .column2,
		.four_columns > .column3,
		.four_columns > .column4 {
			width: 100%;
			float: none;
			margin-bottom: 30px;
		}

		.four_columns > .column1 > .column_inner,
		.four_columns > .column2 > .column_inner,
		.four_columns > .column3 > .column_inner,
		.four_columns > .column4 > .column_inner {
			padding: 0;
		}

		.footer-bottom p,
		.footer-bottom a {
			font-size: 11px;
		}
	}
</style>
