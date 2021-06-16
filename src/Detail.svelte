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
        <li>Ingredient 1: {#if drinkDetails.strMeasure1 != undefined} {drinkDetails.strMeasure1}{/if} {drinkDetails.strIngredient1}</li>
        {/if}
        {#if drinkDetails.strIngredient2 != undefined}
        <li>Ingredient 2: {#if drinkDetails.strMeasure2 != undefined} {drinkDetails.strMeasure2}{/if} {drinkDetails.strIngredient2}</li>
        {/if}
        {#if drinkDetails.strIngredient3 != undefined}
        <li>Ingredient 3: {#if drinkDetails.strMeasure3 != undefined} {drinkDetails.strMeasure3}{/if} {drinkDetails.strIngredient3}</li>
        {/if}
        {#if drinkDetails.strIngredient4 != undefined}
        <li>Ingredient 4: {#if drinkDetails.strMeasure4 != undefined} {drinkDetails.strMeasure4}{/if} {drinkDetails.strIngredient4}</li>
        {/if}
        {#if drinkDetails.strIngredient5 != undefined}
        <li>Ingredient 5: {#if drinkDetails.strMeasure5 != undefined} {drinkDetails.strMeasure5}{/if} {drinkDetails.strIngredient5}</li>
        {/if}
        {#if drinkDetails.strIngredient6 != undefined}
        <li>Ingredient 6: {#if drinkDetails.strMeasure6 != undefined} {drinkDetails.strMeasure6}{/if} {drinkDetails.strIngredient6}</li>
        {/if}
        {#if drinkDetails.strIngredient7 != undefined}
        <li>Ingredient 7: {#if drinkDetails.strMeasure7 != undefined} {drinkDetails.strMeasure7}{/if} {drinkDetails.strIngredient7}</li>
        {/if}
        {#if drinkDetails.strIngredient8 != undefined}
        <li>Ingredient 8: {#if drinkDetails.strMeasure8 != undefined} {drinkDetails.strMeasure8}{/if} {drinkDetails.strIngredient8}</li>
        {/if}
        {#if drinkDetails.strIngredient9 != undefined}
        <li>Ingredient 9: {#if drinkDetails.strMeasure9 != undefined} {drinkDetails.strMeasure9}{/if} {drinkDetails.strIngredient9}</li>
        {/if}
        {#if drinkDetails.strIngredient10 != undefined}
        <li>Ingredient 10: {#if drinkDetails.strMeasure10 != undefined} {drinkDetails.strMeasure10}{/if} {drinkDetails.strIngredient10}</li>
        {/if}
        {#if drinkDetails.strIngredient11 != undefined}
        <li>Ingredient 11: {#if drinkDetails.strMeasure11 != undefined} {drinkDetails.strMeasure11}{/if} {drinkDetails.strIngredient11}</li>
        {/if}
        {#if drinkDetails.strIngredient12 != undefined}
        <li>Ingredient 12: {#if drinkDetails.strMeasure12 != undefined} {drinkDetails.strMeasure12}{/if} {drinkDetails.strIngredient12}</li>
        {/if}
    {drinkDetails.strInstructions}
    </ul>
{/if}  
</main>