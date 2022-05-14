<template>
    <div class="screen">
        <h1>POKE MEMORIES</h1>
        <h3>Select mode to start game</h3>
        <div class="actions">
          <button @click="onStart(16)">
            <span>4X4</span>
            <span>Easy</span>
          </button>
          <button @click="onStart(36)">
            <span>6X6</span>
            <span>Normal</span>
          </button>
          <button @click="onStart(64)">
            <span>8X8</span>
            <span>Hard</span>
          </button>
          <button @click="onStart(100)">
            <span>10X10</span>
            <span>Supper Hard</span>
          </button>
        </div>
        <coppy-right class="coppyright"></coppy-right>
    </div>
</template>

<script>
import CoppyRight from "./CoppyRightCreen.vue"
export default{
    methods: {
      onStart(totalOfBlocks) {
        this.$emit('onStart',{ totalOfBlocks })
      }
    },
    components: {
      CoppyRight
    }
}
</script>

<style scoped>
.screen{
  width: 100%;
  height: 100vh;
  background: var(--dark);
 
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.screen h1{
  font-size: 72px;
  color: var(--light);
}
.screen h3{
  font-size: 32px;
  color: var(--light);
}.actions{
  display: flex;
  flex-direction: row;
}
.actions button{
  font: var(--font);
  width:150px;
  height: 150px;
  margin: 32px 16px 0;
  background: var(--dark);
  color: var(--light); 
  border: 1px solid var(--light);
  border-radius: 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  cursor: pointer;
  transition: background .3s ease-in-out;
}
.actions button:hover{
  background: var(--light);
  color: var(--dark);
}
.actions button span:first-child{
  font-size: 32px;;
}
.coppyright{
  position: fixed;
  left: 50%;
  bottom: 1.5rem;
  transform: translateX(-50%);
}
</style>
