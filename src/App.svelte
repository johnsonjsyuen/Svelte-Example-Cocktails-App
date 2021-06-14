<script>
	import { apiData, drinks } from './store.js';
	import Detail from './Detail.svelte';

	$: ingredient = 'Gin';
	$: visibleArray = [];

	const fetchDrinks = async () => {
	fetch("https://www.thecocktaildb.com/api/json/v1/1/filter.php?i="+ingredient)
	  .then(response => response.json())
	  .then(data => {
			console.log(data);
		apiData.set(data);

		visibleArray = [...$drinks];
	    visibleArray.fill(false,0);
	  }).catch(error => {
		console.log(error);
		return [];
	  });
	}
	
	$:{
		fetchDrinks(ingredient)
	}
	</script>

<main>
	<h1>Whiskey Drinks Menu</h1>
	
	<h2>Filter by ingredient: <input bind:value={ingredient}></h2>
	
	<ul>
	{#each $drinks as drink, i}
	<div 
	on:mouseover={()=>{console.log(i + "over"); visibleArray[i] = true}}
	on:mouseout={()=>{console.log(i + "out"); visibleArray[i] = false}}
    >
		<p>Name:
			<a href={"https://www.thecocktaildb.com/api/json/v1/1/lookup.php?i="+drink.idDrink}>{drink.strDrink}</a>
			<img src={drink.strDrinkThumb+"/preview"} alt={drink.idDrink} width=200 height=200 	
		/>
			<Detail drinkId={drink.idDrink} visible={visibleArray[i]}></Detail>
		</p>
	</div>
		
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