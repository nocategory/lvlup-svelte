<script>
  import { blur } from 'svelte/transition'
  import Question from './Question.svelte'
  import Modal from './Modal.svelte'
  let activeQuestion = 0
  let score = 0
  let isModalOpen = false
  let quiz = getQuiz()

  async function getQuiz() {
    const res = await fetch(
      'https://opentdb.com/api.php?amount=10&category=12&type=multiple'
    )
    const quiz = await res.json()
    return quiz
  }

  function nextQuestion() {
    activeQuestion++
  }

  function resetQuiz() {
    isModalOpen = false
    activeQuestion = 0
    score = 0
    quiz = getQuiz()
  }

  function addScore() {
    score++
  }

  $: if (score > 5 || activeQuestion > 9) {
    isModalOpen = true
  }
</script>

<div>
  <button on:click={resetQuiz}>New Quiz</button>

  <h3>Score: {score}</h3>

  <h3>Question #{activeQuestion + 1}</h3>

  {#await quiz}
    <h4>Loading...</h4>
  {:then data}
    {#each data.results as question, k}
      {#if k === activeQuestion}
        <div in:blur={{ delay: 400 }} out:blur={{ duration: 400 }}>
          <Question {addScore} {nextQuestion} {question}>
            {question}
          </Question>
        </div>
      {/if}
    {/each}
  {/await}
</div>

{#if isModalOpen}
  <Modal>
    <h2>You finished with a score of {score}/10 !</h2>
    <button on:click={resetQuiz}>New Quiz</button>
  </Modal>
{/if}
