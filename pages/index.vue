<template>
  <v-container>
    <v-row justify="center">
      <v-col cols="12" sm="6" md="4">
        <Metronome />
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
import Metronome from '../components/Metronome'
export default {
  components: {
    Metronome
  }
}
</script>
