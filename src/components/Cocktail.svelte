<script lang="ts">
  import { fade } from 'svelte/transition';

  interface Drink {
    strDrinkThumb: string;
    strDrink: string;
    strInstructions: string;
  }

  export let drinkData: Drink;
  const {
    strDrinkThumb: image,
    strDrink: name,
    strInstructions: details,
  } = drinkData;
</script>

<div transition:fade class="card mx-2 my-2 pt-2" style="width: 18rem;">
  <img loading="lazy" src={image} class="card-img-top" alt="..." />
  <div class="card-body">
    <h5 class="card-title">{name}</h5>
    <p class="card-text">
      {details}
    </p>
  </div>
</div>
