<script>
  import { score } from './store.js'
  export let question
  export let nextQuestion

  let isCorrect = false
  let isAnswered = false

  let answers = [
    {
      answer: question.correct_answer,
      correct: true,
    },
    // SPREAD OPERATOR YAYYY
    ...question.incorrect_answers.map((answer) => {
      return {
        answer,
        correct: false,
      }
    }),
  ].sort(() => Math.random() - 0.5)

  function checkAnswer(correct) {
    if (!isAnswered) {
      isCorrect = correct
      isAnswered = true
      correct ? $score++ : null
    }
  }
</script>

<h3>{@html question.question}</h3>

{#if isAnswered}
  <h4 class:isCorrect class:isIncorrect={!isCorrect}>
    {#if isCorrect}
      You got it right!
    {:else}
      You got it wrong!
    {/if}
  </h4>
{/if}

{#each answers as answer}
  <button on:click={() => checkAnswer(answer.correct)} disabled={isAnswered}
    >{@html answer.answer}</button
  >
{/each}

{#if isAnswered}
  <div>
    <button on:click={nextQuestion}>Next Question</button>
  </div>
{/if}

<style>
  h4.isCorrect {
    color: green;
  }
  h4.isIncorrect {
    color: red;
  }
</style>
