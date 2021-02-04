<template>
  <div>
    <h1>Vue.JS Basket</h1>

    <div>
      <h2>Score:</h2>
      <span>{{ this.teams.A.score }}</span> -
      <span>{{ this.teams.B.score }}</span>
    </div>
    </div>
      <button @click="handlePlayerShoot(2)">Shoot 2</button>
      <button @click="handlePlayerShoot(3)">Shoot 3</button>
    <div>

    <div>
      <ul>
        <li v-for="log in logs" :key="log">{{ log }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
function getRandom() {
  return Math.floor(0 + (100 - 0) * Math.random());
}

export default {
  name: "App",
  data() {
    return {
      teams: {
        A: {
          name: "Player",
          score: 0,
        },
        B: {
          name: "Computer",
          score: 0,
        },
      },
      logs: [],
    };
  },
  methods: {
    handleAttempt(points) {
      const difficulty = points === 3 ? 30 : 50;
      return getRandom() < difficulty ? true : false;
    },
    handleScore(team, points) {
      const result = this.handleAttempt(points)
      if(result) {
        this.teams[team].score += points;
        this.handleLog(team, points, "in");
      } else {
        this.handleLog(team, points, "out");
      }
    },
    handleLog(team, points, result) {
      const thisLog = `${this.teams[team].name} shoots ${points}, it's ${result}`;
      this.logs.unshift(thisLog);
    },
    handleComputerShoot() {
      const points = getRandom() > 50 ? 2 : 3;

      setTimeout(() => {
        this.handleScore('B', points);
      }, 500);
    },
    handlePlayerShoot(points) {
      this.handleScore('A', points);
      this.handleComputerShoot();
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
