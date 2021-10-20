<script>
  export let quizName = 'My Quiz'

  let a = 0
  let b = 0
</script>

<div>
  <h2>{quizName}</h2>
  <h1>{a + b}</h1>
  <input type="number" bind:value={a} />
  <input type="number" bind:value={b} />
</div>
