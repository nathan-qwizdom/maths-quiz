<template>
  <div class="notification is-success">
    <div class="content">
      <h1 class="has-text-weight-bold has-text-white">That's Correct!</h1>
      <hr>
      <button class="button has-text-weight-semibold is-medium" @click="onNextQuestion">Next Question</button>
    </div>
  </div>
</template>
<script>
  export default{
    methods: {
      onNextQuestion(){
        this.$emit('confirmed');
      }
    }
  }
</script>
<style>

</style>
