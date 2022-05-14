<template>
    <div class="screen" >
      <div class="screen__inner" 
      :style="{width: `${((((920 - 16*4)/ Math.sqrt(cardsContent.length) -16)*3) /4 +16) * Math.sqrt(cardsContent.length)}px`}"
      >
        <card-flip 
          v-for="(card,index) in cardsContent" 
          :key="index"
          :ref="`card-${index}`"
          :imgBackFaceUrl="`images/${card}.png`"
          :card="{index, value:card}"
          @onFlip="checkRule($event)"
          :cardsContent="cardsContent"
        ></card-flip>
      </div>
    </div>
</template>

<script>
import CardFlip from './Card.vue'

export default{
  data() {
    return {
      rules: []
    }
  },
  props: {
    cardsContent: {
      type: Array,
      default: function() {
        return [];
      }
    }
  },
  methods: {
    checkRule(card) {
      if(this.rules.length === 2) return false;
      this.rules.push(card);
      if(this.rules.length === 2 && this.rules[0].value === this.rules[1].value){
        this.$refs[`card-${this.rules[0].index}`][0].onDisableMode();
        this.$refs[`card-${this.rules[1].index}`][0].onDisableMode();
        this.rules = [];

        const disableElement = document.querySelectorAll('.screen .card.disable');
        if(disableElement && disableElement.length === this.cardsContent.length -2){
          setTimeout(() => {
            
            this.$emit('onFinish');
          },920)
        }
        
      }else if(this.rules.length === 2 && this.rules[0].value !== this.rules[1].value){
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          this.rules = [];
                  


        },800)

      }else return false;

    }
  },
  components: {
    CardFlip,
  }
}
</script>

<style scoped>
  .screen{
    width: 100%;
    height: 920px;
    position: absolute;
    z-index: 2;
    top: 0;
    left: 0;
    background: var(--dark);
    color: var(--light)
  }
  .screen__inner{
    display: flex;
    flex-wrap: wrap;
    margin: 2rem auto;

  }
</style>
