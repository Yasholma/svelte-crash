<script lang="ts">
  import type { IFeedback } from "../interfaces";
  import { FeedbackStore } from "../stores";
  import Card from "./Card.svelte";

  export let feedback: IFeedback;

  const handleDelete = (id: number): void => {
    FeedbackStore.update((current) => current.filter((item) => item.id !== id));
  };
</script>

<Card>
  <div class="num-display">
    {feedback.rating}
  </div>
  <button class="close" on:click={() => handleDelete(feedback.id)}>X</button>
  <div class="text-display">
    {feedback.text}
  </div>
</Card>

<style>
  .num-display {
    position: absolute;
    top: -10px;
    left: -10px;
    width: 50px;
    height: 50px;
    border: 1px #eee solid;
    border-radius: 50%;
    display: grid;
    place-items: center;
    background: #ff6a95;
    color: #fff;
    font-size: 19px;
  }

  .close {
    position: absolute;
    top: 10px;
    right: 20px;
    cursor: pointer;
    background: none;
    border: 1px solid #c91212;
    color: #c91212;
    width: 30px;
    height: 30px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 50%;
    font-size: 0.8rem;
    font-weight: bold;
    transition: all 0.3s ease-in-out;
  }

  .close:hover {
    transform: scale(1.1);
    background: #c91212;
    color: #fff;
  }
</style>
