<script>
  import { createEventDispatcher } from "svelte";
  export let items;
  export let activeTab;

  const dispatch = createEventDispatcher();
</script>

<div class="tabs">
  <ul>
    {#each items as item}
      <li on:click={() => dispatch("tabChange", item)}>
        <div class:active={activeTab === item}>{item}</div>
      </li>
    {/each}
  </ul>
</div>

<style>
  .tabs {
    margin-bottom: 40px;
  }
  ul {
    display: flex;
    justify-content: center;
    padding: 0;
    list-style-type: none;
  }
  li {
    margin: 0 16px;
    color: #555;
    cursor: pointer;
    font-size: 18px;
  }
  .active {
    color: #d91b42;
    border-bottom: 2px solid #d91b42;
    padding-bottom: 8px;
  }
</style>
