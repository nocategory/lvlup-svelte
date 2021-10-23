<script>
  export let question
  export let nextQuestion
  export let addScore

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
      correct ? addScore() : null
    }
  }
</script>

<h3>{@html question.question}</h3>

{#if isAnswered}
  {#if isCorrect}
    <h4>You got it right!</h4>
  {:else}
    <h4>You got it wrong!</h4>
  {/if}
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
