<script>
	import { slide } from "svelte/transition"
  import ChevronToggle from "../ChevronToggle.svelte"
  export let headerText;
  export let expanded = true;
  let toggleExpanded = () => {
    expanded = !expanded;
  };
</script>

<div class="collapsibleSection">
  <collapsibleHeader>
    <button area-expanded={expanded} on:click|preventDefault={toggleExpanded}>
      <h2>{headerText}</h2>
      <ChevronToggle toggled={expanded} size=16/>
    </button>
  </collapsibleHeader>
  {#if expanded}
  <div class="collapsibleContents" hidden={!expanded} transition:slide|local>
      <slot />
  </div>
  {/if}
</div>

<style>
  collapsibleHeader {
    margin: 0;
    padding: 0;
    vertical-align: middle;
  }

  h2 {
    margin: 0;
  }

  button {
    font-size: 14px;
    background-color: var(--grey-100);
    border-radius: 4px;
    color: var(--gray-999);
    display: flex;
    justify-content: space-between;
    width: 100%;
    border: none;
    margin: 0;
    padding: 0.5em 0.5em;
    cursor: pointer;
    /* border: 1px solid var(--grey-200); */
  }

  button[area-expanded="true"] .vert {
    display: none;
  }
  svg {
    margin-top: 0.1em;
    height: 1em;
    width: 1em;
    outline: 1px solid;
  }
 
  .collapsibleContents {
    padding: 0.5em 0.5em 1.5em 0.5em;
  }
  .collapsibleSection {
    padding: 0px;
    margin: 0.5em 0 0 0;
  }
</style>
