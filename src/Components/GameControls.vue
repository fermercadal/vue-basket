<template>
  <div class="vBasket__controls">
      <button @click="playerShoot(2)" :disabled="!active">Shoot 2</button>
      <button @click="playerShoot(3)" :disabled="!active">Shoot 3</button>
    </div>
</template>

<script>
export default {
  name: 'GameControls',
  props: {
    active: {
      type: Boolean,
      required: true,
    }
  },
  emits: {
    'player-shoot': (score) => {
      if(!isNaN(score)) {
        return true;
      } else {
        console.log('score should be a number')
        return false;
      }
    }
  },
  methods: {
    playerShoot(score) {
      this.$emit('player-shoot', score)
    }
  }
}
</script>

<style lang="scss">
.vBasket__controls {
  margin-top: auto;
  padding: 2rem 0 4rem 0;

  button {
    font-size: 1.2rem;
    font-weight: 600;
    margin: 1rem;
    padding: 1rem;
  }
}
</style>