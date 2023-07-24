<script>
  import { push } from 'svelte-spa-router';
  import Nav from './Nav.svelte';
  import { onMount } from 'svelte';
  import axios from 'axios';
  import { selectedCardone } from '../src/store';

  let ships = [];
  let cards = [];
  let selectedCard = null;

  async function goto(shipName, equipmentName) {
    try {
      const response = await axios.get(
        `http://192.168.0.192:5000/ship/equipment/details/${shipName}/${equipmentName}`
      );
      selectedCard = response.data;
      console.log(selectedCard);
      selectedCardone.set(selectedCard);
      localStorage.setItem('mydata', JSON.stringify(selectedCard));
      push('/predict');
    } catch (error) {
      console.error(error);
    }
  }

  const fetch = async () => {
    try {
      const res = await axios.get('http://192.168.0.192:5000/ship/list');
      console.log(res.data);
      ships = res.data.ships;
      console.log(ships, 'response');
    } catch (error) {
      console.error(error);
    }
  };

  const card = async () => {
    try {
      const result = await axios.get('http://192.168.0.192:5000/ships/details');
      cards = result.data.ships;
      console.log(cards, 'result');
      console.log(cards[0]['equipment_details'][0]);
      // console.log(cards[0]['equipment_details'].equipment_name);
    } catch (error) {
      console.error(error);
    }
  };

  onMount(() => {
    fetch();
    card();
  });

  function getHealthColor(health) {
    if (health >= 90) {
      return 'green';
    } else if (health >= 70) {
      return 'orange';
    } else {
      return 'red';
    }
  }
</script>

<Nav />
<div class="container">
  {#each ships as ship}
    <div class="row justify-content-md-center">
      <div class="card col-3">
        <h3>{ship}</h3>
      </div>
    </div>
    <div class="row">
      {#each cards as card}
        {#if card.name === ship}
          {#each card.equipment_details as equipment}
            <div
              class="card-1 col-3"
              style="background-color: {getHealthColor(equipment.health)}"
            >
              <p>{equipment.equipment_name}</p>
              <p>Health: {equipment.health}%</p>
              <p>Last Updated: {equipment.last_updated}</p>
              <button
                type="submit"
                on:click={() => goto(card.name, equipment.equipment_name)}
              >
                View
              </button>
            </div>
          {/each}
        {/if}
      {/each}
    </div>
  {/each}

  {#if selectedCard}
    <div class="card-details">
      <h4>Selected Equipment: {selectedCard.equipment_name}</h4>
      <p>Health: {selectedCard.health}</p>
      <p>Last Updated: {selectedCard.last_updated}</p>
      <p>Ship Name: {selectedCard.ship_name}</p>
    </div>
  {/if}
</div>

<!-- <div class="row">
      {#each cards as card (card.name)}
        {#each card.equipment_details as equipment}
           {#if card.name === equipment.equipmentName} -->
<!-- <div
              class="card-1 col-3"
              style="background-color: {getHealthColor(equipment.health)}"
            >
              <p>{equipment.equipment_name}</p>
              <p>health: {equipment.health}%</p>
              <p>last-updated: {equipment.last_updated}</p>
              <button
                type="submit"
                on:click={() => goto(card.name, equipment.equipment_name)}
              >
                View
              </button>
            </div> -->
<!-- {/if} -->
<!-- {/each}
      {/each}
    </div>
    {#if selectedCard}
      <div class="card-details">
        <h4>Selected Equipment: {selectedCard.equipment_name}</h4>
        <p>Health: {selectedCard.health}</p>
        <p>Last Updated: {selectedCard.last_updated}</p>
        <p>Ship Name: {selectedCard.ship_name}</p>
      </div>
    {/if}
  {/each}
</div> -->

<style>
  .card {
    background-color: #fff;
    border-radius: 4px;
    padding: 1rem;
    box-shadow: 0 2px 4px rgba(249, 246, 246, 0.1);
    margin: 0.5rem;
    width: 250px;
  }

  .card-1 {
    border-radius: 4px;
    padding: 1rem;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    margin: 0.5rem;
    width: 250px;
    float: left;
  }

  .card-1 p {
    color: #fff;
  }
</style>
