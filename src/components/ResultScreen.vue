<template>
  <div class="screen2">
    <h1>✨ Chúc Mừng ✨</h1>
    <h3>Bạn đã hoàn thành trong {{Math.round(timer/1000)}} giây </h3>
    <button @click="onStart">Start Again</button>
  </div>
</template>

<script>


export default {
  props:{
    timer:{
      type:Number,
      required:true,
    }
  },
  methods:{
    onStart(){
      this.$emit('onStart');
    }
  }
};
</script>

<style scoped>
.screen2 {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.screen2 h1 {
  font-size: 5rem;
}

.screen2 h4 {
  margin-top: 1.5rem;
  font-size: 3rem;
}

.screen2 button {
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
  transition: background 0.3s ease-in-out;
}

.screen2 button:hover {
  background-color: var(--light);
  color: var(--dark);
}
</style>
