<template>
  <total-balance :total="totalBalance()"></total-balance>
  <budget-list :list="list"></budget-list>
</template>

<script>
import TotalBalance from '@/components/TotalBalance.vue';
import BudgetList from '@/components/BudgetList.vue';
export default {
  name: 'App',
  components: { BudgetList, TotalBalance },
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
    const totalBalance = () => {
      return Object.values(list).reduce((acc, item) => acc + item.value, 0);
    };

    return {
      list,
      totalBalance,
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
