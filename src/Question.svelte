<script>
  export let question

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

  console.log(answers)

  function handleClick(correct) {
    isCorrect = correct
    isAnswered = true
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
  <button on:click={() => handleClick(answer.correct)} disabled={isCorrect}
    >{@html answer.answer}</button
  >
{/each}
