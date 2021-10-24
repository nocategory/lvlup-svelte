<script>
  import { scale } from 'svelte/transition'
  import { createEventDispatcher } from 'svelte'

  const dispatch = createEventDispatcher()
</script>

<div class="modal-back">
  <div class="modal" transition:scale>
    <slot />
    <button on:click={() => dispatch('close')}>New Quiz</button>
  </div>
</div>

<style>
  .modal-back {
    background-color: rgba(0, 0, 0, 0.5);
    width: 100%;
    position: fixed;
    height: 100%;
    top: 0;
    left: 0;
  }
  .modal {
    background-color: #fff;
    padding: 2rem 4rem;
    border-radius: 1rem;
  }
  .modal-back,
  .modal {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }
</style>
