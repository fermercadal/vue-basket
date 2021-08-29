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
  name: "GameScore",
  props: {
    teams: {
      type: Object,
      required: true,
      validator: (teams) => {
        return Object.keys(teams).length === 2;
      },
    },
  },
};
</script>

<style lang="scss">
.vBasket__team {
  padding: 1rem;
  width: 30%;
}

.vBasket__score {
  display: flex;
  flex-flow: row wrap;
  justify-content: center;

  .score__name {
    font-style: oblique;
    font-weight: 600;
  }

  .score__score {
    font-size: 5rem;
  }
}
</style>
