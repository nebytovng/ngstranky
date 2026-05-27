<script lang="ts">
	type Member = {
		id: string;
		photo: string;
		role: string;
		name: string;
		desc: string;
		tel: { num: string; display: string } | null;
		email: string;
	};

	const row1: Member[] = [
		{
			id: 'jakub',
			photo: '/images/Jakub.svg',
			role: 'ONLINE MARKETING, SEO, SEM, SMO, PPC',
			name: 'Ing. Jakub Vytiska',
			desc: 'Jednatel společnosti. Specialista na online marketing a optimalizaci stránek.',
			tel: { num: '00420608133557', display: '+420 608 133 557' },
			email: 'vytiska@ngstranky.cz',
		},
		{
			id: 'lukas',
			photo: '/images/Lukas.svg',
			role: 'TVORBA WEBU, ESHOPU, PROGRAMOVÁNÍ',
			name: 'Ing. Lukáš Nesvadba',
			desc: 'Jednatel společnosti. Tvůrce specifických řešení a šéf programátorského týmu.',
			tel: { num: '00420775133557', display: '+420 775 133 557' },
			email: 'nesvadba@ngstranky.cz',
		},
		{
			id: 'michal-g',
			photo: '/images/Michal-G.svg',
			role: 'KÓDOVÁNÍ, PROGRAMOVÁNÍ, TVORBA WEBŮ',
			name: 'Michal Gerz',
			desc: 'Kodérská a programátorská činnost. Servis webových stránek a on-line podpora.',
			tel: { num: '00420734160638', display: '+420 734 160 638' },
			email: 'gerz@ngstranky.cz',
		},
		{
			id: 'jiri',
			photo: '/images/Jiri.svg',
			role: 'SOCIÁLNÍ SÍTĚ, EMAILING',
			name: 'Bc. Jiří Ježek',
			desc: 'Specialista sociálních sítí, emailingová on-line podpora klientů.',
			tel: { num: '00420739144636', display: '+420 739 144 636' },
			email: 'jezek@ngstranky.cz',
		},
	];

	const row2: Member[] = [
		{
			id: 'veronika',
			photo: '/images/Veronika.svg',
			role: 'SEO, ANALYTIKA, COPYWRITING',
			name: 'Veronika Hůlková',
			desc: 'SEO specialistka obsahu. Analytika a copywriting.',
			tel: null,
			email: 'hulkova@ngstranky.cz',
		},
		{
			id: 'michal-m',
			photo: '/images/Michal-M.svg',
			role: 'LINKBUILDING, ANALYTIKA',
			name: 'Michal Moravec',
			desc: 'Linkbuilder. Analytická činnost.',
			tel: null,
			email: 'moravec@ngstranky.cz',
		},
		{
			id: 'pavla',
			photo: '/images/Pavla.svg',
			role: 'SPRÁVA OBSAHU, COPYWRITING',
			name: 'Pavla Frühbauerová',
			desc: 'Správce obsahu klientských webů, copywriterská činnost.',
			tel: null,
			email: 'fruhbauerova@ngstranky.cz',
		},
		{
			id: 'renata',
			photo: '/images/Lucie.svg',
			role: 'PPC KAMPANĚ',
			name: 'Renata Novotná',
			desc: 'PPC specialistka',
			tel: null,
			email: 'novotna@ngstranky.cz',
		},
	];

	const rows = [row1, row2];

	let flipped = $state(Array(8).fill(false) as boolean[]);

	function setFlip(i: number, val: boolean) {
		flipped[i] = val;
		flipped = [...flipped];
	}
</script>

<section class="content_section team-section" id="tym">
	<div class="section-wrap">
		<h2>NÁŠ TÝM</h2>
		<p class="intro">Chceme, aby jste věděli, kdo se Vašemu projektu bude věnovat. Ke všem klientům přistupujeme individuálně. Těšíme se na spolupráci.</p>
		<div class="separator transparent" style="margin: 14px 0 10px;"></div>

		{#each rows as row, rowIdx (rowIdx)}
			{#if rowIdx > 0}
				<div class="row-gap"></div>
			{/if}
			<div class="four_columns clearfix">
				{#each row as member, colIdx (member.id)}
					<div class="column{colIdx + 1}">
						<div class="column_inner">

							<!-- Flip karta: přední SVG foto / zadní modrá s rolí -->
							<!-- svelte-ignore a11y_no_static_element_interactions -->
							<div
								class="flip-card"
								class:flipped={flipped[rowIdx * 4 + colIdx]}
								onmouseenter={() => setFlip(rowIdx * 4 + colIdx, true)}
								onmouseleave={() => setFlip(rowIdx * 4 + colIdx, false)}
							>
								<div class="flip-card-inner">
									<div class="flip-front">
										<img src={member.photo} alt={member.name} loading="lazy" />
									</div>
									<div class="flip-back">
										<div class="flip-back-text">
											<h4>{member.role}</h4>
										</div>
									</div>
								</div>
							</div>

							<!-- Info pod kartou -->
							<h4 class="member-name">{member.name}</h4>
							<p class="member-desc">{member.desc}</p>
							<p class="member-contact">
								<small>
									{#if member.tel}
										<a href={'tel:' + member.tel.num} rel="nofollow noopener noreferrer">
											<i class="fa fa-phone" aria-hidden="true"></i>&nbsp;{member.tel.display}
										</a>
										<br />
									{/if}
									<a
										href={'mailto:' + member.email + '?subject=Dotaz%20z%20webu'}
										rel="nofollow noopener noreferrer"
									>
										<i class="fa fa-envelope" aria-hidden="true"></i>&nbsp;{member.email}
									</a>
								</small>
							</p>

						</div>
					</div>
				{/each}
			</div>
		{/each}
	</div>
</section>

<style>
	section.team-section {
		background-color: #fff;
		padding: 80px 0;
	}

	/* Sloupce — stejná struktura jako ClientStats */
	.four_columns > .column1,
	.four_columns > .column2,
	.four_columns > .column3,
	.four_columns > .column4 {
		width: 25%;
		float: left;
	}

	.four_columns > .column1 > .column_inner { padding: 0 16px 0 0; }
	.four_columns > .column2 > .column_inner { padding: 0 10px 0 6px; }
	.four_columns > .column3 > .column_inner { padding: 0 6px 0 10px; }
	.four_columns > .column4 > .column_inner { padding: 0 0 0 16px; }

	/* Mezera mezi řadami (orig: &nbsp;<br>&nbsp;<br>) */
	.row-gap {
		clear: both;
		height: 40px;
	}

	/* -------------------------------------------------------
	   Flip karta
	------------------------------------------------------- */
	.flip-card {
		position: relative;
		cursor: pointer;
		width: 160px;
		height: 160px;
		perspective: 600px;
	}

	.flip-card-inner {
		position: relative;
		width: 100%;
		height: 100%;
		transform-style: preserve-3d;
		transition: transform 0.5s ease-in-out;
	}

	.flip-card.flipped .flip-card-inner {
		transform: rotateY(180deg);
	}

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
		padding: 20px;
		box-sizing: border-box;
	}

	.flip-back-text h4 {
		font-family: 'Oswald', sans-serif;
		font-size: 20px;
		line-height: 24px;
		font-weight: 500;
		color: #fff;
		text-align: center;
		margin: 0;
	}

	/* -------------------------------------------------------
	   Info pod kartou
	------------------------------------------------------- */
	h2 {
		font-family: 'Oswald', sans-serif;
		font-size: 40px;
		line-height: 40px;
		font-weight: 500;
		color: #262626;
		margin: 0 0 20px;
	}

	.intro {
		font-family: 'PT Sans', sans-serif;
		font-size: 13px;
		line-height: 22px;
		color: #4f4f4f;
		margin: 10px 0;
	}

	.member-name {
		font-family: 'Oswald', sans-serif;
		font-size: 20px;
		line-height: 20px;
		font-weight: 500;
		color: #262626;
		margin: 16px 0 6px;
	}

	.member-desc {
		font-family: 'PT Sans', sans-serif;
		font-size: 13px;
		line-height: 22px;
		color: #4f4f4f;
		margin: 0 0 6px;
	}

	.member-contact {
		font-family: 'PT Sans', sans-serif;
		font-size: 13px;
		line-height: 22px;
		color: #4f4f4f;
		margin: 0;
	}

	.member-contact a {
		color: #4f4f4f;
		text-decoration: none;
	}

	.member-contact a:hover {
		color: #3c8eba;
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
			margin-bottom: 40px;
		}

		.four_columns > .column1 > .column_inner,
		.four_columns > .column2 > .column_inner,
		.four_columns > .column3 > .column_inner,
		.four_columns > .column4 > .column_inner {
			padding: 0;
		}

		h2 { font-size: 28px; line-height: 32px; }
	}
</style>
