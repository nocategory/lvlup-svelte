<script>
  let result
  let correctAnswer = 'c'
  const answers = ['a', 'b', 'c', 'd']

  function checkAnswer(answer) {
    return answer === correctAnswer
      ? (result = 'Correct!!!!')
      : (result = 'Wrong DUH!')
  }
</script>

<div>
  {#if result}
    <h1>{result}</h1>
  {:else}
    <h2>Pick an answer!</h2>
  {/if}
  {#each answers as answer}
    <button on:click={() => checkAnswer(answer)}
      >Answer {answer.toUpperCase()}</button
    >
  {/each}
</div>
