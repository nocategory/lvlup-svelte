<script>
  let result
  let correctAnswer = 'c'
  const answers = ['a', 'b', 'c', 'd']
  let quiz = getQuiz()

  function checkAnswer(answer) {
    return answer === correctAnswer
      ? (result = 'Correct!!!!')
      : (result = 'Wrong DUH!')
  }

  async function getQuiz() {
    const res = await fetch(
      'https://opentdb.com/api.php?amount=10&category=12&type=multiple'
    )
    const quiz = await res.json()
    return quiz
  }

  const handleClick = () => (quiz = getQuiz())
</script>

<div>
  <button on:click={handleClick}>Get Quiz</button>
  {#await quiz}
    <h4>Loading...</h4>
  {:then data}
    <h2>{data.results[0].question}</h2>
  {/await}

  {#if result}
    <h4>{result}</h4>
  {:else}
    <h4>Pick an answer!</h4>
  {/if}

  {#each answers as answer}
    <button on:click={() => checkAnswer(answer)}
      >Answer {answer.toUpperCase()}</button
    >
  {/each}
</div>
