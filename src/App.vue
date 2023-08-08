<template>
  <h1>Restaurant</h1>
  <button
    @click="send('FETCH')"
    :disabled="!(state.matches('ready') || state.matches('initial'))"
  >
    FETCH
  </button>

  <button
    @click="send('RETRY')"
    :disabled="!state.matches('failure')"
  >
    RETRY
  </button>

  <span v-show="state.matches('loading')">...Loading...</span>

  <div
    v-if="
    state.matches('ready') ||
    state.matches('success') ||
    state.matches('loading')
  ">
    <div :key="restaurant.id" v-for="restaurant in state.context.restaurants">
      <h3>{{ restaurant.name }}</h3>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { useMachine } from '@xstate/vue'
import fetchMachine from './fetchMachine'

export default defineComponent({
  name: 'App',
  setup() {
    const { state, send } = useMachine(fetchMachine, { devTools: true })

    return {
      state,
      send,
    }
  },
})
</script>

<style scoped>
  h1 {
    color: white;
  }
  button {
    margin: 10px;
  }
</style>
