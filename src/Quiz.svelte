<script>
  import Question from './Question.svelte'
  let activeQuestion = 0
  let score = 0
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
    activeQuestion = 0
    score = 0
    quiz = getQuiz()
  }

  function addScore() {
    score++
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
        <Question {addScore} {nextQuestion} {question}>
          {question}
        </Question>
      {/if}
    {/each}
  {/await}
</div>
