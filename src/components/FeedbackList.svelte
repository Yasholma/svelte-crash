<script lang="ts">
  import { fade, scale } from "svelte/transition";
  import { FeedbackStore } from "../stores";
  import FeebackItem from "./FeedbackItem.svelte";
</script>

{#each $FeedbackStore as feedback (feedback.id)}
  <div in:scale out:fade={{ duration: 500 }}>
    <FeebackItem {feedback} />
  </div>
{/each}
