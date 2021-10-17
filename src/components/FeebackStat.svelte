<script lang="ts">
  import { FeedbackStore } from "../stores";

  $: count = $FeedbackStore.length;
  $: average =
    $FeedbackStore.reduce((a, { rating }) => a + rating, 0) /
    $FeedbackStore.length;
</script>

<div class="feedback-stat">
  <h4>{count} Reviews</h4>
  <h4>Ratings Average: {average || 0}</h4>
</div>

<style>
  .feedback-stat {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
</style>
