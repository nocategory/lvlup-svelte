<script>
  let result = ''
  let correctAnswer = 'c'

  function checkAnswer(answer) {
    return answer === correctAnswer
      ? (result = 'Correct!!!!')
      : (result = 'Wrong DUH!')
  }
</script>

<div>
  <h1>{result}</h1>
  <button on:click={() => checkAnswer('a')}>Answer A</button>
  <button on:click={() => checkAnswer('b')}>Answer B</button>
  <button on:click={() => checkAnswer('c')}>Answer C</button>
  <button on:click={() => checkAnswer('d')}>Answer D</button>
</div>
