<script>
  let result
  let correctAnswer = 'c'
  const answers = ['a', 'b', 'c', 'd']

  function checkAnswer(answer) {
    return answer === correctAnswer
      ? (result = 'Correct!!!!')
      : (result = 'Wrong DUH!')
  }

  async function getQuiz() {
    const res = await fetch(
      'https://opentdb.com/api.php?amount=10&category=12&type=multiple'
    )
    const data = await res.json()
  }
</script>

<div>
  <button on:click={getQuiz}>Get Quiz</button>
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
