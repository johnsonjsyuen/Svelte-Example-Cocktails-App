<script>
    import { DataTable } from "carbon-components-svelte";
    export let drinkId;
    export let visible;
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
    {#if visible === true}
    <h3>{drinkDetails.strDrink}</h3>
    <img src={drinkDetails.strDrinkThumb+"/preview"} alt={drinkDetails.idDrink} width=200 height=200/>
    <ul>
        {#if drinkDetails.strIngredient1 != undefined}
        <li>Ingredient 1: {drinkDetails.strMeasure1} {drinkDetails.strIngredient1}</li>
        {/if}
        {#if drinkDetails.strIngredient2 != undefined}
        <li>Ingredient 2: {drinkDetails.strMeasure2} {drinkDetails.strIngredient2}</li>
        {/if}
        {#if drinkDetails.strIngredient3 != undefined}
        <li>Ingredient 3: {drinkDetails.strMeasure3} {drinkDetails.strIngredient3}</li>
        {/if}
        {#if drinkDetails.strIngredient4 != undefined}
        <li>Ingredient 4: {drinkDetails.strMeasure4} {drinkDetails.strIngredient4}</li>
        {/if}
        {#if drinkDetails.strIngredient5 != undefined}
        <li>Ingredient 5: {drinkDetails.strMeasure5} {drinkDetails.strIngredient5}</li>
        {/if}
        {#if drinkDetails.strIngredient6 != undefined}
        <li>Ingredient 6: {drinkDetails.strMeasure6} {drinkDetails.strIngredient6}</li>
        {/if}
    </ul>
{/if}  
</main>