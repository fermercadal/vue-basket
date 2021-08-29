<template>
  <div class="vBasket">
    <h1>vBasket</h1>

    <section v-if="!start && !over" class="vBasket__start">
      <button @click="startGame">Start</button>
    </section>

    <section v-if="start" class="vBasket__game">
      <GameScore :teams="teams" />
      <GameLogs :logs="logs" />
      <GameControls @player-shoot="handlePlayerShoot" :active="possesion"/>
    </section>

    <section v-if="over" class="vBasket__over">
      <GameScore :teams="teams" />
      <p><strong>{{ winner }}</strong> wins!</p>
      <button @click="playAgain">Play Again</button>
    </section>
  </div>
</template>

<script>
import GameScore from './Components/GameScore.vue';
import GameLogs from './Components/GameLogs.vue';
import GameControls from './Components/GameControls.vue';

const getRandom = () => {
  return Math.floor(0 + (100 - 0) * Math.random());
}

export default {
  name: "App",
  data() {
    return {
      start: false,
      over: false,
      teams: {
        A: {
          name: 'Player',
          score: 0,
        },
        B: {
          name: 'Computer',
          score: 0,
        },
      },
      possesion: true,
      logs: [],
      winner: null,
    };
  },
  components: {
    GameScore,
    GameLogs,
    GameControls,
  },
  watch: {
    teams: {
      deep: true,
      handler(teams) {
        if(teams.A.score >= 10) {
          this.handleWin(teams.A.name)
        }
        if(teams.B.score >= 10) {
          this.handleWin(teams.B.name)
        }
      }
    }
  },
  methods: {
    startGame() {
      this.start = true;
    },
    handleAttempt(score) {
      const difficulty = score === 3 ? 30 : 50;
      return getRandom() < difficulty;
    },
    handleScore(team, score) {
      const result = this.handleAttempt(score);
      if(result) {
        this.teams[team].score += score;
        this.handleLog(team, score, 'in');
      } else {
        this.handleLog(team, score, 'out');
      }
      this.possesion = false;
    },
    handleLog(team, score, result) {
      const thisLog = `${this.teams[team].name} shoots ${score}, it's ${result}`;
      this.logs.unshift(thisLog);
    },
    handleComputerShoot() {
      const score = getRandom() > 50 ? 2 : 3;

      setTimeout(() => {
        this.handleScore('B', score);
        this.possesion = true;
      }, 800);
    },
    handlePlayerShoot(score) {
      this.handleScore('A', score);
      if (!this.winner) {
        this.handleComputerShoot();
      }
    },
    handleWin(team) {
      this.over = true;
      this.start = false;
      this.winner = team;
    },
    playAgain() {
      this.over = false;
      this.start = true;
      this.winner = null;
      this.logs = [];
      this.teams.A.score = 0;
      this.teams.B.score = 0;
    },
  },
};
</script>

<style lang="scss">
body {
  font-size: 16px;
  margin: 0;
  padding: 0;
}
* {
  box-sizing: content-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  
  .vBasket {
    display: flex;
    flex-flow: column;
    height: 100vh;
    overflow: hidden;
    text-align: center;
    width: 100vw;
  }

  h1 {
    font-size: 1.4rem;
    font-style: oblique;
    font-weight: 700;
    margin: 0;
    padding: 2rem 0;
    width: 100%;
  }

  .vBasket__game {
    display: flex;
    flex-direction: column;
    height: calc(100vh - 90px);
  }
}
</style>
