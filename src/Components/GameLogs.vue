<template>
  <div class="vBasket__logs">
      <ul>
        <li v-for="log in logs" :key="log">{{ log }}</li>
      </ul>
    </div>
</template>

<script>
export default {
  name: 'GameLogs',
  props: {
    logs: {
      type: Array,
      required: true,
    }
  },
}
</script>

<style lang="scss">
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
</style>