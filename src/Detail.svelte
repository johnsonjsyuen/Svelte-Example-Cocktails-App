<script>
    import { DataTable } from "carbon-components-svelte";
    export let drinkId;
    let drinkDetails = {};

    const fetchDrinkDetail = async (drinkId) => {
	fetch("https://www.thecocktaildb.com/api/json/v1/1/lookup.php?i="+drinkId)
	  .then(response => response.json())
	  .then(data => {
			console.log(data);
            drinkDetails = data.drinks[0];
	  }).catch(error => {
		console.log(error);
		return [];
	  });
	}
	
	$:{
		fetchDrinkDetail(drinkId)
	}
</script>

<main>
    {drinkId}
    {#if drinkDetails.strIngredient1 != undefined}
        Ingredient 1:{drinkDetails.strIngredient1}
    {/if}
    {#if drinkDetails.strIngredient2 != undefined}
        Ingredient 2:{drinkDetails.strIngredient2}
    {/if}
    {#if drinkDetails.strIngredient3 != undefined}
        Ingredient 3:{drinkDetails.strIngredient3}
    {/if}
    {#if drinkDetails.strIngredient4 != undefined}
        Ingredient 4:{drinkDetails.strIngredient4}
    {/if}
    {#if drinkDetails.strIngredient5 != undefined}
        Ingredient 5:{drinkDetails.strIngredient5}
    {/if}
    {#if drinkDetails.strIngredient6 != undefined}
        Ingredient 6:{drinkDetails.strIngredient6}
    {/if}

    <DataTable
  headers={[{ key: 'ingredient', value: 'ingredient' }, { key: 'Name', value: 'Name' }]}
  rows={[{ ingredient: 'a', name: 'Load Balancer 3'}]}
/>
</main>