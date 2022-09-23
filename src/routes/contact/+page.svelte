<script lang="ts">
	let formData: object = {}
	let isSubmitted: boolean = false

	const encode = (data: object): string => {
		return Object.keys(data)
			.map(key => encodeURIComponent(key) + '=' + encodeURIComponent(data[key]))
			.join('&')
	}

	const handleSubmit = (e: Event): void => {
		const target = e.target as HTMLFormElement
		fetch('/', {
				method: 'POST',
				headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
				body: encode({
					'form-name': target.getAttribute('name'),
					...formData,
				}),
			})
			.then(() => { isSubmitted = true })
			.catch(error => alert(error))
	}
</script>


<svelte:head>
	<title>Josh Collinsworth | Contact</title>
	<meta data-key="description" name="description" content="If you fill out this form, I'll probably send you an email. What a bargain!">
	<meta property="og:image" content="https://joshcollinsworth.com/images/site-image.png" />
	<meta name="twitter:image" content="https://joshcollinsworth.com/images/site-image.png"/>
</svelte:head>

<div class="compressed-content">
	{#if !isSubmitted}

		<noscript>
			<h2>Sorry, this contact form won't work without JavaScript enabled.</h2>
			<p>You can try me at <code>joshuajcollinsworth</code> on the good ol' Google mail instead if you like.</p>
		</noscript>

		<form
			id="contact-form"
			name="contact"
			method="post"
