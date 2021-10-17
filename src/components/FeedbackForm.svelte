<script lang="ts">
  import { v4 as uuid } from "uuid";
  import { FeedbackStore } from "../stores";
  import Button from "./Button.svelte";
  import Card from "./Card.svelte";
  import RatingSelect from "./RatingSelect.svelte";

  let text = "";
  let rating = 10;
  let isFormInvalid = true;
  let min = 10;
  let message = "";

  const handleInput = () => {
    if (text.trim().length < min) {
      message = `Text must be at least ${min} characters`;
      isFormInvalid = true;
    } else {
      message = "";
      isFormInvalid = false;
    }
  };

  const handleRatingSelect = ({ detail }) => (rating = detail);

  const handleSubmit = () => {
    if (text.trim().length > min) {
      const newFeedback = {
        id: uuid(),
        text,
        rating: +rating,
      };

      FeedbackStore.update((current) => {
        return [newFeedback, ...current] as any;
      });
      text = "";
    }
  };
</script>

<Card>
  <header>
    <h2>How would you rate your service with us?</h2>
  </header>
  <form on:submit|preventDefault={handleSubmit}>
    <RatingSelect on:rating-selected={handleRatingSelect} />
    <div class="input-group">
      <input
        on:input={handleInput}
        bind:value={text}
        type="text"
        placeholder="Tell us something that keeps you coming back"
      />
      <Button type="submit" disabled={isFormInvalid}>Send</Button>
    </div>
    {#if message}
      <div class="message">{message}</div>
    {/if}
  </form>
</Card>

<style>
  header {
    max-width: 400px;
    margin: auto;
  }
  header h2 {
    font-size: 22px;
    font-weight: 600;
    text-align: center;
  }
  .input-group {
    display: flex;
    flex-direction: row;
    border: 1px solid #ccc;
    padding: 8px 10px;
    border-radius: 8px;
    margin-top: 15px;
  }
  input {
    flex-grow: 2;
    border: none;
    font-size: 16px;
  }
  input:focus {
    outline: none;
  }
  .message {
    padding-top: 10px;
    text-align: center;
    color: rebeccapurple;
  }
</style>
