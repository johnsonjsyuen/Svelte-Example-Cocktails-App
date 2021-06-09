<script>
	import { onMount } from "svelte";
	import { apiData, drinks } from './store.js';

	$: ingredient = 'Gin';

	const fetchDrinks = async () => {
	fetch("https://www.thecocktaildb.com/api/json/v1/1/filter.php?i="+ingredient)
	  .then(response => response.json())
	  .then(data => {
			console.log(data);
		apiData.set(data);
	  }).catch(error => {
		console.log(error);
		return [];
	  });
	}
	
	//onMount(async () => fetchDrinks(ingredient));
	$:{
		fetchDrinks(ingredient)
	}
	</script>

<main>
	<h1>Whiskey Drinks Menu</h1>
	<h2>Filter by ingredient: <input bind:value={ingredient}></h2>
	
	<ul>
	{#each $drinks as drink}
		<p>Name:<a href={"https://www.thecocktaildb.com/api/json/v1/1/lookup.php?i="+drink.idDrink}>{drink.strDrink}</a>
			<img src={drink.strDrinkThumb+"/preview"} alt={drink.idDrink}/></p>
	{/each}
	</ul>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	p {
		color: #ff3e00;
		text-transform: none;
		font-size: 2em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>