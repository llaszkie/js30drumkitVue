<template>
  <div :ref="'divElm' + singleKey.id" @transitionend="removeTransition($event)">
    <kbd>{{ singleKey.letter }}</kbd>
    <span>{{ singleKey.sound }}</span>
    <audio :ref="'audioElm' + singleKey.id" :src="singleKey.audio"></audio>
  </div>
</template>

<script>
  export default {
    props: ['singleKey'],
    methods: {
      playSound: function (e) {
        if (e.keyCode === this.singleKey.id) {
          let refAudio = this.$refs['audioElm' + this.singleKey.id]
          refAudio.currentTime = 0
          refAudio.play()

          let refDiv = this.$refs['divElm' + this.singleKey.id]
          refDiv.classList.add('playing')
        }
      },
      removeTransition: function (e) {
        if (e.propertyName === 'transform') {
          let refDiv = this.$refs['divElm' + this.singleKey.id]
          refDiv.classList.remove('playing')
        }
      }
    },
    created () {
      window.addEventListener('keydown', this.playSound)
    }
  }

</script>

<style scoped>
  kbd {
    font-size: 4rem;
    display: block;
  }

  div {
    border: .4rem solid black;
    border-radius: .5rem;
    margin: 1rem;
    padding: 1rem .5rem;
    color: white;
    width: 10rem;
    text-align: center;
    background: rgba(0, 0, 0, 0.4);
    text-shadow: 0 0 0.5rem black;
    transition: all .07s ease;
  }

  span {
    color: #ffc600;
    font-size: 1.2rem;
    text-transform: uppercase;
    letter-spacing: .1rem;
  }

  .playing {
    transform: scale(1.1);
    border-color: #ffc600;
    box-shadow: 0 0 1rem #ffc600;
  }
</style>
