<template>
  <div class="card"
       :class = "{'disabled':isDisabled }" 
       :style = "{
           height: `${(1080 - 16*4 ) / Math.sqrt(cardContext.length) -16}px`,
           width: `${((1080 - 16*4 ) / Math.sqrt(cardContext.length) -16)*3/4}px`,
       }">
      <div class="card__inner" :class = "{'is-flipped':isFlipped }" @click=" onToggleFlip">
          <div class="card_face card_face_front">
              <div class="card_content"></div>
          </div>
          <div class="card_face card_face_back" >
              <div class="card_content" :style="{backgroundImage: `url(${require('@/assets/' + imgBackUrl)})`}"></div>
          </div>
      </div>
  </div>
</template>

<script>


export default {
  props:{
      card: {
        type: Object,
        },
      imgBackUrl:{
          type: String,
          require:true
        },
      cardContext:{
          type: Array,
          default: function(){
              return [];
          }
      }
  },
  data() {
      return {
          isDisabled: false,
          isFlipped: false
      }
  },
  methods: {
      onToggleFlip(){
          if(this.isDisabled) return false;
          this.isFlipped = !this.isFlipped;
          if(this.isFlipped){
              this.$emit('onFlip', this.card)
          }
      },
      closeFlip() {
          this.isFlipped= false;
      },
      openFlip() {
          this.isDisabled = true;
      }
  },
};
</script>

<style lang="css" scoped>
.card{
    display: inline-block;
    margin-right: 1rem;
    margin-bottom: 1rem;
    perspective: 120px;
    
}
.card__inner{
    height:100%;
    width: 100%;
    transition: transform 1s;
    transform-style: preserve-3d;
    cursor: pointer;
    position: relative;
}
.card.disabled .card__inner{
    cursor: default;
}
.card__inner.is-flipped {
  transform: rotateY(-180deg);
}

.card_face{
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
    overflow: hidden;
    border-radius:1rem;
    padding:1rem;
    box-shadow: 0 3px 18px 3px rgba(0,0,0,0.2);
}
.card_face_back{
    background-color: var(--light);
    transform: rotateY(-180deg)
}
.card_face_front .card_content{
    background: url('../assets/images/icon_back.png') no-repeat center center ;
    background-size: contain ;
    width: 100%;
    height: 100%;
}
.card_face_back .card_content{
    background:no-repeat center center ;
    background-size: contain ;
    width: 100%;
    height: 100%;

}
</style>
