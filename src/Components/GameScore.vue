<template>
  <div class="vBasket__score">
      <div class="vBasket__team" v-for="team in teams" :key="team.name">
        <div class="score__name">
          {{ team.name }}
        </div>
        <div class="score__score">
          {{ team.score }}
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'GameScore',
  props: {
    teams: {
      type: Object,
      required: true,
    }
  },
}
</script>

<style>

</style>