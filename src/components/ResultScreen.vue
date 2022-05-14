<template>
    <div class="screen-result">
      <h1>✨ Congratulations ✨</h1>
      <p>{{ Math.round(timer/1000) }} seconds</p>
      <button @click="onStartAgain">Start again</button>
      <coppy-right class="coppyright"></coppy-right>
    </div>
</template>

<script>
import CoppyRight from "./CoppyRightCreen.vue"
export default{
  props: {
    timer: {
      type: Number,
      required: true
    }
  },
  methods: {
    onStartAgain() {
      this.$emit("onStartAgain");
    }
  },
  components: {
    CoppyRight
  }
    
}
</script>

<style scoped>
.screen-result{
  background: var(--dark);
  color: var(--light);
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
h1{
  font-size: 80px;
}
p{
  font-size: 48px;
}
button{
    font: var(--font);
    background: transparent;
    box-shadow: none;
    border: 1px solid var(--light);
    color: var(--light);
    margin: 1rem;
    padding: 1rem 1.25rem;
    border-radius: 0.5rem;
    font-size: 1.25rem;
    cursor: pointer;
    transition: background .3s ease-in-out;
}
button:hover{
  background: var(--light);
  color: var(--dark);
}
.coppyright{
  position: fixed;
  left: 50%;
  bottom: 1.5rem;
  transform: translateX(-50%);
  font-size: 24px;
}

</style>
