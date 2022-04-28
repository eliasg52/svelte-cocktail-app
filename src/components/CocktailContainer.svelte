<script lang="ts">
  import axios from 'axios';
  import Cocktail from './Cocktail.svelte';

  let drinks: Array<any>;
  let drinkName: string;

  const getDrinks = async (name: string = 'margarita') => {
    const { data } = await axios.get(
      `https://www.thecocktaildb.com/api/json/v1/1/search.php?s=${name}`
    );
    drinks = data.drinks;
    console.log(drinks);
    return data;
  };

  let promise = getDrinks();

  const handleSubmit = () => {
    promise = getDrinks(drinkName);
    drinkName = '';
  };
</script>

<div class="container text-center mt-3">
  <h2>Search Cocktail</h2>

  <form on:submit|preventDefault={handleSubmit}>
    <input bind:value={drinkName} type="text" class="p-1" />
    <button class="btn btn-danger">Search</button>
  </form>

  {#await promise}
    <div class="text-center">
      <div class="spinner-border" role="status">
        <span class="visually-hidden">Loading...</span>
      </div>
    </div>
  {:then drinksResponse}
    <div class="row">
      {#each drinks as drink}
        <Cocktail drinkData={drink} />
      {/each}
    </div>
  {/await}
</div>
