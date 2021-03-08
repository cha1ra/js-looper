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
    <v-card-actions>
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
    </v-card-actions>
  </v-card>
</template>
<script>
export default {
  data () {
    return {
      tempo: 60,
      clicking: false,
      timeoutId: null
    }
  },
  methods: {
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
      console.log('click!')
      if (this.clicking) {
        this.timeoutId = setTimeout(this.click, 1000)
      }
    }
  }
}
</script>
