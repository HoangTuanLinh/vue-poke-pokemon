<template>
    <div class="card" 
    :class="{disable : isDefault}"
    :style="{height: `${(920 - 16*4)/ Math.sqrt(cardsContent.length) -16}px`,
    width: `${(((920 - 16*4)/ Math.sqrt(cardsContent.length) -16)*3) /4}px`
    }"
    >
      <div class="card__inner" :class="{ 'is-flipped': isFlipped, }" @click="onToggelFlipCard">
        <div class="card__face card__face--front">
          <div class="card-content" 
          :style="{backgroundSize: `${(((920 - 16*4)/ Math.sqrt(cardsContent.length) -16)*3) /4/3}px 
          ${(((920 - 16*4)/ Math.sqrt(cardsContent.length) -16)*3) /4/3}px`
          
          
          }"></div>
        </div>
        <div class="card__face card__face--back">
          <div class="card-content" :style="{ backgroundImage: `url(${require('@/assets/' + imgBackFaceUrl)})` }"></div>
        </div>
      </div>
    </div>
</template>

<script>
export default{
  props: {
    imgBackFaceUrl: {
      type: String,
      required: true
    },
    card: {
      type: [String, Array, Number, Object],
    },
    cardsContent: {
      type: Array,
      default: function() {
        return [];
      }
    }
  },
  data() {
    return {
      isDefault:false,
      isFlipped: false,
    }
  },
  methods: {
    onToggelFlipCard() {
      if(this.isDefault) return false;
      this.isFlipped = !this.isFlipped;
      if(this.isFlipped) this.$emit("onFlip", this.card)
    },
    onFlipBackCard() {
        this.isFlipped = false;
    },
    onDisableMode() {
      this.isDefault = true;
    }
  }
}
</script>

<style scoped>
  .card{
    display: inline-block;
    margin-right: 1rem;
    margin-bottom: 1rem;
  }
  .card__inner{
    width: 100%;
    height:100%;
    transition: transform 1s;
    transform-style: preserve-3d;
    cursor: pointer;
    position: relative;
  }
  .card__inner.is-flipped{
    transform: rotateY(-180deg);
  }
  .card__face{
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
    overflow: hidden;
    border-radius: 1rem;
    padding: 1rem;
    box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
  }
  .card__face--front .card-content{
    background: url(../assets/images/icon_back.png) no-repeat center center;
    height: 100%;
    width: 100%;
  }
  .card__face--back .card-content{
    background-repeat: no-repeat;
    background-position: center center;
    background-size: contain;
    height: 100%;
    width: 100%;
  }
  .card__face--back{
    background: var(--light);
    transform: rotateY(-180deg);
  }
  .card.disable .card__inner{
    cursor: default;
  }
</style>
