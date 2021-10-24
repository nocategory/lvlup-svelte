<script>
  import { scale } from 'svelte/transition'
</script>

<div class="modal-back">
  <div class="modal" transition:scale>
    <slot />
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
