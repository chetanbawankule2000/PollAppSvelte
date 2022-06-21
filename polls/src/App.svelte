<script>
  import Header from "./components/Header.svelte";
  import Footer from "./components/Footer.svelte";
  import Tabs from "./shared/Tabs.svelte";
  import CreatePollForm from "./components/CreatePollForm.svelte";
  import Pollist from "./components/Pollist.svelte";

  let items = ["Current Polls", "Add New Poll"];
  let activeTab = "Current Polls";

  const tabChange = (e) => {
    activeTab = e.detail;
  };

  // polls
  let polls = [];

  const addPoll = (e) => {
    activeTab = "Current Polls";
  };
</script>

<Header />
<main>
  <Tabs {items} {activeTab} on:tabChange={tabChange} />
  {#if activeTab === "Current Polls"}
    <Pollist />
  {:else if activeTab === "Add New Poll"}
    <CreatePollForm on:addPoll={addPoll} />
  {/if}
</main>
<Footer />

<style>
  main {
    max-width: 960px;
    margin: 40px auto;
  }
</style>
