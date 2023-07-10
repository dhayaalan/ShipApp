<script>
  // import axios from 'axios';
  import Nav from './Nav.svelte';
  import { selectedCardone } from '../src/store';
  import { onMount } from 'svelte';

  let data = [];
  let selectedCardData = null;

  onMount(() => {
    selectedCardone.subscribe((value) => {
      selectedCardData = value;
      console.log(selectedCardData, 'erfghjk');
    });
  });
</script>

<Nav />
<!-- <table>
  <thead>
    <tr>
      <th>Serial No</th>
      <th>Updated Time</th>
      <th>Parameter 1</th>
      <th>Parameter 2</th>
    </tr>
  </thead>
  <tbody>
    {#each data as item}
      <tr>
        <td>{item.serialNo}</td>
        <td>{item.updateTime}</td>
        <td>{item.parameter1}</td>
        <td>{item.parameter2}</td>
      </tr>
    {/each}
  </tbody>
</table> -->
{#if selectedCardData}
  <table>
    <thead>
      <tr>
        <th>Equipment Name</th>
        <th>Metric1</th>
        <th>Metric2</th>
        <th>Metric3</th>
        <th>Metric4</th>
        <th>Metric5</th>
        <th>Metric6</th>
        <th>Metric7</th>
        <th>Metric8</th>
        <th>Metric9</th>
        <th>Metric10</th>
        <th>Timestamp</th>
      </tr>
    </thead>
    <tbody>
      {#each selectedCardData as data}
        <tr>
          <td>{data.equipment_name}</td>
          <td>{data.metric1}</td>
          <td>{data.metric2}</td>
          <td>{data.metric3}</td>
          <td>{data.metric4}</td>
          <td>{data.metric5}</td>
          <td>{data.metric6}</td>
          <td>{data.metric7}</td>
          <td>{data.metric8}</td>
          <td>{data.metric9}</td>
          <td>{data.metric10}</td>
          <td>{data.timestamp}</td>
        </tr>
      {/each}
    </tbody>
  </table>
{/if}
<div class="credit">
  <div class="gauge">
    <div class="gauge__body">
      <div class="gauge__fill" />
      <div class="gauge__cover" />
    </div>
  </div>
  <p>Prediction Score</p>
</div>

<style>
  .gauge {
    width: 100%;
    max-width: 250px;
    font-family: 'Roboto', sans-serif;
    font-size: 32px;
    color: #004033;
  }

  .gauge__body {
    width: 100%;
    height: 0;
    padding-bottom: 50%;
    background: #b4c0be;
    position: relative;
    border-top-left-radius: 100% 200%;
    border-top-right-radius: 100% 200%;
    overflow: hidden;
  }

  .gauge__fill {
    position: absolute;
    top: 100%;
    left: 0;
    width: inherit;
    height: 100%;
    background: #5072fa;
    transform-origin: center top;
    transform: rotate(0.25turn);
    transition: transform 0.2s ease-out;
  }

  .gauge__cover {
    width: 75%;
    height: 150%;
    background: #ffffff;
    border-radius: 50%;
    position: absolute;
    top: 25%;
    left: 50%;
    transform: translateX(-50%);

    /* Text */
    display: flex;
    align-items: center;
    justify-content: center;
    padding-bottom: 25%;
    box-sizing: border-box;
  }
  .credit {
    padding: 75px 450px;
  }

  p {
    padding: 10px 70px;
    font-weight: bold;
  }

  table {
    /* border-collapse: collapse; */
    width: 100%;
    margin: 8px;
    align-items: center;
  }

  th,
  td {
    padding: 8px;
    text-align: center;
    border-bottom: 1px solid #ccc;
  }

  th {
    background-color: #d9d9d9;
    font-weight: bold;
  }

  tr:hover {
    background-color: #5072fa;
  }
</style>
