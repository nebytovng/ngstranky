<script lang="ts">
	let status: 'idle' | 'sending' | 'ok' | 'error' = $state('idle');

	let jmeno = $state('');
	let email = $state('');
	let tel = $state('');
	let zprava = $state('');

	async function handleSubmit(e: SubmitEvent) {
		e.preventDefault();
		status = 'sending';

		try {
			/* Odeslání na původní WordPress endpoint — funguje jako proxy,
			   pro SvelteKit static build je třeba nahradit vlastním API. */
			const fd = new FormData();
			fd.append('jmeno', jmeno);
			fd.append('your-email', email);
			fd.append('tel', tel);
			fd.append('zprava', zprava);

			const res = await fetch('https://www.ngstranky.cz/wp-json/contact-form-7/v1/contact-forms/2997/feedback', {
				method: 'POST',
				body: fd,
			});

			status = res.ok ? 'ok' : 'error';
		} catch {
			status = 'error';
		}
	}
</script>

<section class="content_section quick-contact" id="kontakt">
	<div class="section-wrap">
	<div class="two_columns_25_75 clearfix">
		<div class="column1">
			<div class="column_inner">
				<h2>RYCHLÝ KONTAKT</h2>
			</div>
		</div>
		<div class="column2">
			<div class="column_inner">
				<img
					class="imgcontact"
					src="/images/sipka-uvod.png"
					alt="Chcete atraktivní a moderní www stránky? Napište nám."
					loading="lazy"
				/>
			</div>
		</div>
	</div>

	<div class="separator transparent" style="margin: 5px 0;"></div>

	<form class="formular" onsubmit={handleSubmit} novalidate>
		<table>
			<tbody>
				<tr>
					<td colspan="1">
						<input
							type="text"
							name="jmeno"
							bind:value={jmeno}
							placeholder="Vaše jméno"
							required
							aria-label="Vaše jméno"
						/>
					</td>
					<td rowspan="2" colspan="2" class="area">
						<textarea
							name="zprava"
							bind:value={zprava}
							placeholder="Vaše zpráva, požadavek, nezávazný dotaz, cokoliv Vás napadne.."
							rows="7"
							aria-label="Zpráva"
						></textarea>
					</td>
				</tr>
				<tr>
					<td colspan="1">
						<input
							type="email"
							name="your-email"
							bind:value={email}
							placeholder="Váš e-mail"
							required
							aria-label="Váš e-mail"
						/>
					</td>
				</tr>
				<tr>
					<td>
						<input
							type="tel"
							name="tel"
							bind:value={tel}
							placeholder="Váš telefon"
							aria-label="Váš telefon"
						/>
					</td>
					<td>
						<button type="submit" disabled={status === 'sending'}>
							{status === 'sending' ? 'Odesílám…' : 'Odeslat'}
						</button>
					</td>
				</tr>
			</tbody>
		</table>

		{#if status === 'ok'}
			<p class="form-msg ok">Děkujeme! Zpráva byla úspěšně odeslána.</p>
		{:else if status === 'error'}
			<p class="form-msg error">Odeslání se nezdařilo, zkuste to prosím znovu.</p>
		{/if}
	</form>
	</div>
</section>

<style>
	section.quick-contact {
		background-color: #fff;
		padding: 80px 0;
	}

	/* Sloupce: 25 % | 75 % */
	.two_columns_25_75 { width: 100%; }
	.two_columns_25_75 > .column1 { width: 25%; float: left; }
	.two_columns_25_75 > .column2 { width: 75%; float: left; }
	.column_inner { padding: 0 20px; }

	h2 {
		font-family: 'Oswald', sans-serif;
		font-size: 40px;
		line-height: 40px;
		font-weight: 500;
		color: #262626;
		margin: 0 0 20px;
	}

	/* Obrázek šipky v pravém sloupci */
	.column2 .column_inner {
		text-align: right;
	}

	.imgcontact {
		max-width: 100%;
		height: auto;
		display: inline-block;
		margin-top: -30px;
	}

	/* --- Formulář (tabulkový layout z originálu) --- */
	.formular {
		width: 100%;
	}

	table {
		width: 100%;
		border-collapse: collapse;
	}

	td {
		padding: 4px 6px 4px 0;
		vertical-align: middle;
	}

	td.area {
		vertical-align: middle;
		padding-left: 10px;
	}

	/* Vstupní pole */
	input[type='text'],
	input[type='email'],
	input[type='tel'] {
		font-family: 'Oswald', sans-serif;
		font-size: 15px;
		font-weight: 300;
		border: 0;
		background-color: #3c8eba;
		height: 40px;
		line-height: 40px;
		color: #fff;
		width: 92%;
		padding: 5px 4%;
		outline: 0;
		display: block;
		transition: background-color 0.2s ease;
	}

	input[type='text']::placeholder,
	input[type='email']::placeholder,
	input[type='tel']::placeholder {
		color: rgba(255, 255, 255, 0.75);
	}

	input[type='text']:focus,
	input[type='email']:focus,
	input[type='tel']:focus {
		background-color: #2e7299;
	}

	textarea {
		font-family: 'Oswald', sans-serif;
		font-size: 15px;
		font-weight: 300;
		border: 0;
		background-color: #3c8eba;
		color: #fff;
		width: 100%;
		padding: 10px 4%;
		outline: 0;
		resize: vertical;
		min-height: 160px;
		display: block;
		box-sizing: border-box;
		transition: background-color 0.2s ease;
	}

	textarea::placeholder {
		color: rgba(255, 255, 255, 0.75);
	}

	textarea:focus {
		background-color: #2e7299;
	}

	/* Tlačítko Odeslat */
	button[type='submit'] {
		font-family: 'Oswald', sans-serif;
		font-size: 13px;
		font-weight: 500;
		text-transform: uppercase;
		letter-spacing: 1px;
		background-color: #e91b23;
		color: #fff;
		border: 0;
		padding: 10px 20px;
		cursor: pointer;
		transition: background-color 0.2s ease;
		white-space: nowrap;
	}

	button[type='submit']:hover:not(:disabled) {
		background-color: #c0151c;
	}

	button[type='submit']:disabled {
		opacity: 0.6;
		cursor: default;
	}

	/* Status zprávy */
	.form-msg {
		margin-top: 14px;
		font-family: 'PT Sans', sans-serif;
		font-size: 13px;
		padding: 8px 12px;
	}

	.form-msg.ok    { background-color: #dff0d8; color: #3c763d; }
	.form-msg.error { background-color: #f2dede; color: #a94442; }

	/* --- Responsive --- */
	@media screen and (max-width: 1024px) {
		.two_columns_25_75 > .column1,
		.two_columns_25_75 > .column2 {
			width: 100%;
			float: none;
		}

		.column2 .column_inner { text-align: left; }
		.imgcontact { display: none; }
	}
</style>
