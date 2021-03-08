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
      clicking: false
    }
  },
  methods: {
    setClicking (flag) {
      this.clicking = flag
      flag && this.click()
    },
    click () {
      console.log('click!')
      this.clicking && setTimeout(this.click, 1000)
    }
  }
}
</script>
