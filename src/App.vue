<template>
  <div class="vBasket">
    <h1>vBasket</h1>

    <div class="vBasket__score">
      <div class="vBasket__team" v-for="team in this.teams" :key="team.name">
        <div class="score__name">
          {{ team.name }}
        </div>
        <div class="score__score">
          {{ team.score }}
        </div>
      </div>
    </div>

    <div class="vBasket__logs">
      <ul>
        <li v-for="log in logs" :key="log">{{ log }}</li>
      </ul>
    </div>

    <div class="vBasket__controls">
      <button @click="handlePlayerShoot(2)" :disabled="!possesion">Shoot 2</button>
      <button @click="handlePlayerShoot(3)" :disabled="!possesion">Shoot 3</button>
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
      possesion: true
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
      this.possesion = false;
    },
    handleLog(team, points, result) {
      const thisLog = `${this.teams[team].name} shoots ${points}, it's ${result}`;
      this.logs.unshift(thisLog);
    },
    handleComputerShoot() {
      const points = getRandom() > 50 ? 2 : 3;

      setTimeout(() => {
        this.handleScore('B', points);
        this.possesion = true;
      }, 800);
    },
    handlePlayerShoot(points) {
      this.handleScore('A', points);
      this.handleComputerShoot();
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
    padding: 3rem 0 2rem 0;
    width: 100%;
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

  .vBasket__team {
    padding: 1rem;
    width: 30%;
  }

  .vBasket__logs {
    font-size: .9rem;
    overflow-y: auto;
    padding: 1rem;

    ul {
      margin: 0;
      padding: 0;
    }
    
    li {
      list-style-type: none;
      padding: .2rem 0;

      &:first-child {
        font-size: 1.1rem;
        font-weight: 600;
      }
    }
    
  }

  .vBasket__controls {
    margin-top: auto;
    padding: 2rem 0;

    button {
      margin: 1rem;
      padding: 1rem;
    }
  }
}
</style>
