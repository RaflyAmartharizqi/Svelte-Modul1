<script>
	import Surname from "./Surname.svelte";
	let namasaya = "ooppp";
	import UserInfo from "./UserInfo.svelte";	
	import Box from "./Box.svelte";
	let stringToRender = "";
	let displayInfoMessage = false;
	import { slide, fade } from "svelte/transition";
	import {onMount} from 'svelte';
	
	let count= 0;
	$: squared = count ** 2;
	$: squaredMinusOne = squared -1;
	function handleClick(){
		count += 1;
	}

	let cities = [
		{
			id: "2323",
			name: "Malang"
		},
		{
			id: "2424",
			name: "Pasuruan"
		},
		{
			id: "2525",
			name: "Sidoarjo"
		},
		{
			id: "2626",
			name: "Batu"
		},
	]

	let characters =[];

	onMount(async () => {
		const apiResponse = await fetch ("https://swapi.dev/api/people/");
		const swPeopleJSON = await apiResponse.json();

		characters = swPeopleJSON.results;

		return () =>console.log('Destroyed');
	});


async function getRandomStarWarsCharacter() {
	const randomNumber = Math.floor(Math.random() * 10) + 1;
	const apiResponse = await fetch(
		`https://swapi.dev/api/people/${randomNumber}/`
	);	
	return await apiResponse.json();
}
let promise = getRandomStarWarsCharacter();




let nama;

function buttonClick(){
	alert("Hello " + nama);
}
function handleInput(event) {
	nama = event.target.value;
}



import { store } from "./store";
import Incrementer from "./Incrementer.svelte";
import Decrementer from "./Decrementer.svelte";
import {bounceInOut} from "svelte/easing";



import { tweened } from "svelte/motion";

const progress = tweened(0, {
	duration:5000,
});
</script>

<main>
	<h1>Hello {namasaya.toUpperCase()}!</h1>
	<h1 class="headerText">Hello {namasaya}!</h1>
	<Surname />
	<UserInfo namaku={'Supardi'} surnamaku={'Desi'}/>
	<Box>
		<h1>Halo Lurrr</h1>
		<p>Wen sambadi lopmi epriting was beutipul</p>
	</Box>
	<Box>
		<h1 slot="header">Halo Lurrr</h1>
		<span slot="footer">Halo Lurrr Footer</span>
	</Box>
	<textarea bind:value={stringToRender} />
	<div>
		{@html stringToRender}
	</div>
	<br>
	<br>
	<form>
	<div class = "name-field">
		<label for="name"> Nama : </label>
		<input type="text" name="name" />
	</div>
	<div class = "Surname-field">
		<label for="surname"> Surnama : </label>
		<input type="text" name="surname" />
	</div>
	<label>	
		<input type="checkbox" bind:checked={displayInfoMessage} />
		Do you want to give me a billion dollars?
	</label>
	</form>

{#if displayInfoMessage}
	<h1 transition:fade>Suwon!</h1>
{/if}


	<button on:click={handleClick}>Counter: {count}</button> 
	<h1>Square of the counter is {squared}</h1>
		<h1>Square of the counter minus one is {squaredMinusOne}</h1>


	<h1>Jatim Cities</h1>
	<ul>
		{#each cities as {id, name}, index}
			<li>{index +1}: {name} (id: {id})</li>
		{/each}
	</ul>

	<ul>
		{#each characters as {name, height, birth_year }}
		<li>
			<strong>{name}</strong>
			(height: {height}cm, birth_year: {birth_year})
		</li>
		{:else}
		<p>Loading...</p>
		{/each}
	</ul>


<!-- <h1>{!character ? 'Loading ...' : character.name}</h1> -->

{#await promise}
	<h1>Loading...</h1>
{:then character}
	<h1>{character.name}</h1>
{/await}


<h1>Introduce yourself:</h1>
<input type="text" on:change={ handleInput } />
<button on:click|preventDefault|once={buttonClick}>Click me</button>






<h1>The count is {$store}</h1>

<Incrementer />
<Decrementer />




<h1>Installing Windows 95...</h1>
<progress value={$progress} />
<sub>2 Weeks remaining...</sub>

<button on:click={() => progress.set(0)}> 0% </button>
<button on:click={() => progress.set(0.75)}> 75% </button>
<button on:click={() => progress.set(1.0)}> 100% </button>

{#if $progress === 1.0}
	<h1>Windows 95 installed, Hore</h1>
{/if}

</main>





<style>
	.headerText {
		color: powderblue;
		font-family: "Comic Sans MS";
	}
	textarea {
		width: 50%;
		height : 200px;
		height: 12 rem;
	}
	progress {
		display:block;
		width:100%;
	}
</style>
