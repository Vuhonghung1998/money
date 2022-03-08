<template>
  <div class="screen1">
      <h1>POKEMON</h1>
      <p>Vui lòng chọn chế độ</p>
      <div class="modes">
          <button @click="onStart(16)">
              <span>Dễ</span>
          </button>
          <button @click="onStart(36)">
              <span>Trung Bình</span>
          </button>
          <button @click="onStart(64)">
              <span>Khó</span>
          </button>
          <button @click="onStart(100)">
              <span>Cực Khó</span>
          </button>
      </div>
  </div>
</template>

<script>


export default {
  methods:{
      onStart(totalOfBlock){
          this.$emit('onStart',{totalOfBlock});
      }
  }
};
</script>

<style>
.screen1 {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  background-color: var(--dark);
  color: var(--light);
}

.screen1 h1 {
  font-size: 4.5rem;
  text-transform: uppercase;
}

.screen1 p {
  font-size: 2rem;
}

.modes {
  display: flex;
  margin-top: 2rem;
}

.modes button {
  font: var(--font);
  width: 150px;
  height: 150px;
  background: transparent;
  box-shadow: none;
  border: 1px solid var(--light);
  color: var(--light);
  display: flex;
  flex-direction: column;
  border-radius: 1rem;
  margin: 0 1rem;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background 0.3s ease-in-out;
}

.modes button:hover {
  background-color: var(--light);
  color: var(--dark);
}

.modes button span:first-child {
  font-size: 2rem;
}

.modes button span:last-child {
  display: block;
  font-size: 1.25rem;
  margin-top: 0.5rem;
}
</style>
