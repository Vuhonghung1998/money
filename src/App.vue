<template>
  <div class="container">
      <main-app 
      v-if="statusMatch === 'default'" 
      @onStart = "onHandleBeforeStart($event)"/>
      <interact-app 
      v-if="statusMatch === 'match'"
      :cardContext = "setting.cardContext"
      @onFinish="onFinish"/>
      <result-app
      v-if="statusMatch === 'result'"
      :timer = "timer"
      @onStart="statusMatch= 'default'"/>
      <copy-right-app />
  </div>
</template>
<script>

import MainScreen from "./components/MainScreen.vue"
import InteractScreen from "./components/InteractScreen.vue"
import ResultScreen from "./components/ResultScreen.vue"
import CopyRight from "./components/CopyRightScreen.vue"
import {randomm} from "./utils/Array.js"
export default {
  name: "App",
  components: {
    MainApp: MainScreen,
    InteractApp: InteractScreen,
    ResultApp: ResultScreen,
    CopyRightApp:CopyRight
  },
  data(){
    return{
      setting:{
        totalOfBlock: 0,
        cardContext : [],//Mang sau cung
        startedAt:null
      },
      statusMatch: "default",
      timer: 0,
    }
  },
  methods: {
    onHandleBeforeStart(config){
      console.log("Running.........",config);
      this.setting.totalOfBlock = config.totalOfBlock;
      const firstCards = Array.from({length: this.setting.totalOfBlock /2},(_,i)=>i+1);
      const secondCards = [...firstCards];
      const cards =[...firstCards,...secondCards];
      console.log(cards);
      this.statusMatch = "match";
      this.setting.cardContext = randomm(randomm(randomm(cards)));
      this.setting.startedAt = new Date().getTime();
      console.log(this.setting.cardContext);
    },
    onFinish(){
      //lấy thời gian
        this.timer = new Date().getTime() - this.setting.startedAt;

      //chuyển sang trang kq
        this.statusMatch = "result";
    }
  },
};
</script>

<style>

</style>
