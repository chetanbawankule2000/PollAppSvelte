<script>
  import PollDetails from "./PollDetails.svelte";
  import PollStore from "../stores/Pollstore.js";
  import { scale, slide, fade } from "svelte/transition";
  import { flip } from "svelte/animate";
</script>

<div class="poll-list">
  {#each $PollStore as poll (poll.id)}
    <div in:fade out:scale|local animate:flip={{ duration: 500 }}>
      <PollDetails {poll} />
    </div>
  {/each}
</div>

<style>
  .poll-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }
</style>
