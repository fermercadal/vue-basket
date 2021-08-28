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

<style>

</style>