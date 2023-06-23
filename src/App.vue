<template>
  <h1>Restaurant</h1>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { useMachine } from '@xstate/vue'
import fetchMachine from './fetchMachine'

export default defineComponent({
  name: 'App',
  setup() {
    const { state, send } = useMachine(fetchMachine, { devTools  : true })
  },
})
</script>

<style scoped>
  h1 {
    color: white;
  }
</style>
