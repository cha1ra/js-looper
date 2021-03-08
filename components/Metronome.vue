<template>
  <v-card
    color="grey lighten-4"
  >
    <v-card-text class="pt-12">
      <v-slider
        v-model="tempo"
        thumb-label="always"
        max="240"
        min="40"
      />
    </v-card-text>
    <v-card-actions class="d-flex justify-space-between">
      <div>
        <v-btn
          color="primary"
          class="font-weight-bold"
          @click="setClicking(true)"
        >
          開始
        </v-btn>
        <v-btn
          color="error"
          class="font-weight-bold"
          @click="setClicking(false)"
        >
          停止
        </v-btn>
      </div>
      <div
        :class="{'flash-light__active': flash}"
      >
        ●
      </div>
    </v-card-actions>
  </v-card>
</template>
<script>
export default {
  data () {
    return {
      tempo: 60,
      clicking: false,
      flash: false,
      timeoutId: null,
      oscillator: null
    }
  },
  computed: {
    offsetMs () {
      return Math.round(1000 * 60 / this.tempo)
    }
  },
  mounted () {
    this.initOscillator()
  },
  methods: {
    initOscillator () {
      const audioCtx = new (window.AudioContext || window.webkitAudioContext)()
      this.oscillator = audioCtx.createOscillator()
      this.oscillator.frequency.value = 440
      this.oscillator.connect(audioCtx.destination)
    },
    setClicking (flag) {
      this.clicking = flag
      if (flag) {
        this.click()
      } else {
        this.timeoutId !== null && clearTimeout(this.timeoutId)
        this.timeoutId = null
      }
    },
    click () {
      this.flashLight()
      if (this.clicking) {
        this.timeoutId = setTimeout(this.click, this.offsetMs)
      }
    },
    flashLight () {
      this.flash = true
      this.oscillator.start()
      setTimeout(() => {
        this.flash = false
        this.oscillator.stop()
        this.initOscillator()
      }, 80)
    }
  }
}
</script>
<style scoped lang="scss">
  .flash-light__active {
    color: orangered;
  }
</style>
