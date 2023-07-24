<script>
  // import axios from 'axios';
  import Nav from './Nav.svelte';
  import { selectedCardone } from '../src/store';
  import { onMount } from 'svelte';
  import Speedometer from 'svelte-speedometer';

  let data = [];
  let selectedCardData = null;

  onMount(() => {
    const savedData = localStorage.getItem('mydata');
    if (savedData) {
      selectedCardData = JSON.parse(savedData);
      selectedCardone.set(selectedCardData);
    }
  
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

<div class="meter">
  <Speedometer
    maxValue={100}
    value={100}
    needleColor="red"
    startColor="red"
    segments={10}
    endColor="green"
  />
</div>

<style>
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
  .meter {
    padding-left: 325px;
  }
</style>
