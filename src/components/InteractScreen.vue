<template>
  <div class="screen">
     <div class="screen_inner"
          :style = "{
                width: `${((((1080 - 16 * 4 ) / Math.sqrt(cardContext.length) -16) * 3)/4 + 16 )*Math.sqrt(cardContext.length)}px`,
                height: `${(((1080 - 16 * 4 ) / Math.sqrt(cardContext.length) -16)  + 16 )*Math.sqrt(cardContext.length) +64}px`,
                
            }">
       <app-card 
        v-for="(card, index) in cardContext" 
        :key="index" 
        :ref="`card-${index}`"
        :imgBackUrl="`images/${card}.png`"
        :card="{ index, value: card }"
        :cardContext="cardContext"
        @onFlip="checkFlip($event)" 
     />
     </div>
  </div>
</template>

<script>
import Card from "./Card.vue";
export default {
  props: {
    cardContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: {
    AppCard: Card,
  },
   data() {
    return {
      rules:[],
    };
  },
  methods: {
    checkFlip(card){
      if(this.rules.length === 2) return false;
      this.rules.push(card);
      if(this.rules.length === 2 && this.rules[0].value === this.rules[1].value){
        console.log("Right......");
        this.$refs[`card-${this.rules[0].index}`][0].openFlip();
        this.$refs[`card-${this.rules[1].index}`][0].openFlip();
        this.rules = [];

        //tạo điều kiện để game hoàn thành
        const disabledElememt = document.querySelectorAll('.screen .card.disabled');
        if(disabledElememt && disabledElememt.length === this.cardContext.length -2 ){
          setTimeout(() =>{
            this.$emit('onFinish');
          },800)
        }
      }else if(this.rules.length === 2 && this.rules[0].value !== this.rules[1].value){
        console.log("Wrongg......");
        //console.log( this.$refs[`card-${this.rules[0].index}`][0])
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].closeFlip();
          this.$refs[`card-${this.rules[1].index}`][0].closeFlip();
          this.rules = [];
        }, 800);
        
      }else return false;
    }
  },
};
</script>

<style lang="css" scoped>
.screen{
  width:100% ;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
}
.screen_inner{
  display: flex;
  margin: 2rem auto;
  flex-wrap: wrap;
}
</style>
