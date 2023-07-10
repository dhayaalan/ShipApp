<script>
  import { push } from 'svelte-spa-router';
  import Nav from './Nav.svelte';
  import { onMount } from 'svelte';
  import axios from 'axios';
  import { selectedCardone } from '../src/store';
  // import { loginUsername } from '../src/store';

  let ships = [];

  let cards = [];
  let selectedCard = null;

  async function goto(shipName, equipmentName) {
    try {
      const response = await axios.get(
        `http://192.168.1.209:5000/ship/equipment/details/${shipName}/${equipmentName}`
      );
      selectedCard = response.data;
      console.log(selectedCard);
      selectedCardone.set(selectedCard);
      push('/predict');
    } catch (error) {
      console.error(error);
    }
  }
  // push('/predict');

  const fetch = async () => {
    const res = await axios({
      method: 'get',
      url: 'http://192.168.1.209:5000/ship/list',
    });
    console.log(res.data);
    ships = res.data.ships;
    console.log(ships, 'response');
  };

  const card = async () => {
    const result = await axios({
      method: 'get',
      url: 'http://192.168.1.209:5000/ships/details',
    });
    cards = result.data.ships;
    console.log(cards, 'result');
    console.log(cards[0]['equipment_details'][0]);
  };

  onMount(() => {
    fetch();
    card();
  });
</script>

<Nav />
<div class="container">
  {#each ships as ship}
    <div class="row justify-content-md-center">
      <div class="card col-3">
        <h3>{ship}</h3>
        <!-- <p>{ship.description}</p> -->
      </div>
    </div>
    <div class="row">
      {#each cards as card (card.name)}
        <!-- <div class="card-1 col-3" key={card.name}> -->
        {#each card.equipment_details as equipment}
          <div class="card-1 col-3">
            <p>{equipment.equipment_name}</p>
            <p>{equipment.health}</p>
            <p>{equipment.last_updated}</p>
            <button
              type="submit"
              on:click={() => goto(card.name, equipment.equipment_name)}
              >View</button
            >
          </div>
        {/each}

        <!-- </div> -->
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
</div>

<style>
  .card {
    background-color: #fff;
    border-radius: 4px;
    padding: 1rem;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    margin: 0.5rem;
    width: 250px;
  }

  .card-1 {
    background-color: #fff;
    border-radius: 4px;
    padding: 1rem;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    margin: 0.5rem;
    width: 250px;
    float: left;
  }
</style>
