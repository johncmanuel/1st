<script lang="ts">
  import type { ContributorMarkdownEntry } from "../types";
  import { Canvas } from "@threlte/core";
  import Starfield from "./Starfield.svelte";
  import ContributorPopup from "./ContributorPopup.svelte";
  import ContributorScene from "./ContributorScene.svelte";
  import Contributors from "./Contributors.svelte";

  export let contributors: ContributorMarkdownEntry[];

  let isContributorDialogOpen = false;
  let contributorIndex = 0;

  function openContributorDialog(i: number) {
    contributorIndex = i;
    isContributorDialogOpen = true;
  }

  $: contributor = contributors[contributorIndex];
</script>

{#key contributorIndex}
  <ContributorPopup bind:contributor bind:isOpen={isContributorDialogOpen} />
{/key}

<Starfield />

<div class="canvas-wrapper">
  <Canvas>
    <ContributorScene {contributors} {openContributorDialog} />
  </Canvas>
</div>

<div class="contributors-grid">
  <h2>List Of Contributors</h2>
  <Contributors {contributors} />
</div>

<style>
  .canvas-wrapper {
    width: 95%;
    margin-inline: auto;
  }

  .contributors-grid {
    width: 80%;
    margin-top: 3rem;
    margin-inline: auto;
  }

  .contributors-grid > h2 {
    text-align: center;
  }
</style>
