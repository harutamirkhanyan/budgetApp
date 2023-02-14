<template>
  <budget-list :list="list"></budget-list>
</template>

<script>
import BudgetList from '@/components/BudgetList.vue';
export default {
  name: 'App',
  components: { BudgetList },
  setup() {
    const list = {
      1: {
        type: 'INCOME',
        value: 100,
        comment: 'Some comment',
        id: 1,
      },
      2: {
        type: 'OUTCOME',
        value: -50,
        comment: 'Some outcome comment',
        id: 2,
      },
    };

    return {
      list
    };
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
<style scoped>
.budget-list-wrap {
  max-width: 500px;
  margin: 0 auto;
}
</style>
