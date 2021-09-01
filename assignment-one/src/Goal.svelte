<script>
  export let goal;
</script>

<h1 class:red__text={goal.includes('!!!')}>GOAL: {goal}</h1>

<style>
    .red__text {
        color: red;
    }
</style>