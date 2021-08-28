<template>
  <div class="vBasket__controls">
      <button @click="playerShoot(2)">Shoot 2</button>
      <button @click="playerShoot(3)">Shoot 3</button>
    </div>
</template>

<script>
export default {
  name: 'GameControls',
  methods: {
    playerShoot(score) {
      this.$emit('player-shoot', score)
    }
  }
}
</script>

<style>

</style>