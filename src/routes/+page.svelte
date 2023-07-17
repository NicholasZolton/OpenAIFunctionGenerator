<script lang='ts'>
	import { base } from "$app/paths";

	interface parameter {
		name: string,
		type: string,
		description: string
	}

	let function_name = "";
	let function_description = "";
	let function_parameters: parameter[] = [];
	let generated_function = "";


	function add_parameter(event: MouseEvent & { currentTarget: EventTarget & SVGSVGElement; }) {
		function_parameters = [
			...function_parameters,
			{
				name: "",
				type: "",
				description: ""
			}
		]
	}

	function remove_parameter(index: number) {
		return function() {
			function_parameters = [
				...function_parameters.slice(0, index),
				...function_parameters.slice(index + 1)
			]
		}
	}

	function generate_function() {

		let function_properties: any = {}

		for (let parameter of function_parameters) {
			function_properties[parameter.name] = {
				"type": parameter.type,
				"description": parameter.description
			}
		}

		let function_json = {
			name: function_name,
			description: function_description,
			parameters: {
				"type": "object",
				"properties": function_properties
			}
		}

		generated_function = JSON.stringify(function_json, null, 4);
	}

</script>

<main>
	<div id="creation-form">
		<hgroup>
			<h1 style="margin-bottom: 0px;">Create Your Function</h1>
			<h1 style="margin: 0px;"><a href="{base}/info">What is this tool?</a></h1>
		</hgroup>
		<h3>Name of the function:</h3>
		<input type="text" bind:value={function_name} />
		
		<h3>Description of the function:</h3>
		<textarea bind:value={function_description}></textarea>

		<h1 style="margin: 0px;">Parameters</h1>

		{#each function_parameters as {name, type, description}, index}
			<div class="parameter">
				<h6>Name of Parameter:</h6>
				<input type="text" bind:value={name} />

				<h6>Type of Parameter:</h6>
				<input type="text" bind:value={type} />

				<h6>Description of Parameter:</h6>
				<textarea bind:value={description} />

				<div id="remove-row" class="{'' + index}">
					<!-- svelte-ignore a11y-click-events-have-key-events -->
					<!-- svelte-ignore a11y-no-static-element-interactions -->
					<svg id="trash-icon" on:click={remove_parameter(index)} xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 448 512"><!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M135.2 17.7L128 32H32C14.3 32 0 46.3 0 64S14.3 96 32 96H416c17.7 0 32-14.3 32-32s-14.3-32-32-32H320l-7.2-14.3C307.4 6.8 296.3 0 284.2 0H163.8c-12.1 0-23.2 6.8-28.6 17.7zM416 128H32L53.2 467c1.6 25.3 22.6 45 47.9 45H346.9c25.3 0 46.3-19.7 47.9-45L416 128z"/></svg>
				</div>
			</div>

			<hr>
			<hr id="dark-hr" />
			<hr>
		{/each}

		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<!-- svelte-ignore a11y-no-static-element-interactions -->
		<svg style="margin: 10px;" id="add-parameter-button" on:click={add_parameter} xmlns="http://www.w3.org/2000/svg" height="3em" viewBox="0 0 512 512"><!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM232 344V280H168c-13.3 0-24-10.7-24-24s10.7-24 24-24h64V168c0-13.3 10.7-24 24-24s24 10.7 24 24v64h64c13.3 0 24 10.7 24 24s-10.7 24-24 24H280v64c0 13.3-10.7 24-24 24s-24-10.7-24-24z"/></svg>

		<!-- svelte-ignore missing-declaration -->
		<button on:click={generate_function}>Generate JSON</button>

		{#if generated_function != ""}
			<h1>Generated Function</h1>
			<textarea>{generated_function}</textarea>
		{/if}

	</div>
</main>

<style>

	a {
		color: inherit;
	}

	hgroup {
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	#trash-icon {
		transition: 0.2s;
		cursor: pointer;
		color: #1095c1;
	}

	#trash-icon:hover {
		fill: #08769b;
	}

	#remove-row {
		display: flex;
		justify-content: flex-end;
	}

	#add-parameter-button {
		margin: 20px;
		transition: 0.2s;
		cursor: pointer;
		color: #1095c1;
	}

	#add-parameter-button:hover {
		fill: #08769b;
	}

	button {
		margin: 20px;
	}

	#dark-hr {
		width: 100%;
		/* make the line slightly darker */
		filter: brightness(30%);
	}

	.parameter {
		width: 100%;
	}

	h6 {
		margin: 10px;
	}

	h3 {
		margin: 10px;
	}

	h1 {
		margin: 20px;
	}

	#creation-form {
		display: flex;
		flex-direction: column;
		align-items: center;
		width: 40%;

		/* add drop shadow here */
		box-shadow: 0px 0px 10px 0px rgba(0,0,0,0.75);		
		border-radius: 10px;
		padding: 30px;
		margin: 50px;
	}

	main {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		width: 100vw;
		overflow-x: hidden;
	}
</style>