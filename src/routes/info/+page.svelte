<script>
	import { base } from "$app/paths";
</script>

<main>

	<a href="{base}/">
		<svg id="back-arrow" xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 512 512"><!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M512 256A256 256 0 1 0 0 256a256 256 0 1 0 512 0zM231 127c9.4-9.4 24.6-9.4 33.9 0s9.4 24.6 0 33.9l-71 71L376 232c13.3 0 24 10.7 24 24s-10.7 24-24 24l-182.1 0 71 71c9.4 9.4 9.4 24.6 0 33.9s-24.6 9.4-33.9 0L119 273c-9.4-9.4-9.4-24.6 0-33.9L231 127z"/></svg>
	</a>

	<h1>What is this tool?</h1>
	<p>
		This tool is designed to help you generate the JSON used in the
		<a target="_blank" href="https://platform.openai.com/docs/api-reference/chat/create#chat/create-functions">
		OpenAI's API syntax for Function Calling</a>. 
	</p>

	<img id="solo-image" src="{base + "/filled_out_form.png"}" alt="Example of filled out form." />

	<p>
		All you have to do is fill out the form, hit
		the "Generate" button, and copy the JSON that
		is generated into your "functions" array
		for the OpenAI call.
	</p>

	<div id="image-row">
		<img src="{base + "/CopyJSON.png"}" alt="Example of copying JSON." />
		<img src="{base + "/showing_api_call.png"}" alt="Example of pasting JSON." />
	</div>

</main>

<style>

	#back-arrow {
		position: absolute;
		top: 30px;
		left: 30px;
	}

	#image-row {
		width: 100%;
		display: flex;
		flex-direction: row;
		justify-content: space-evenly;
		align-items: center;
		margin-bottom: 30px;
	}

	#image-row img {
		max-width: 30%;
	}

	#solo-image {
		max-height: 50%;
	}

	p {
		width: 50%;
		text-align: center;
		margin: 30px;
	}

	h1 {
		margin: 30px;
	}

	main {
		display: flex;
		flex-direction: column;
		align-items: center;

		width: 100vw;
		height: 100vh;
		overflow-x: hidden;
	}
</style>