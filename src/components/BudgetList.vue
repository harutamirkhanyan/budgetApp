<template>
  <div class="budget-list-wrap">
    <el-card class="box-card" :header="header">
      <template v-if="!isEmpty()">
        <div class="list-item" v-for="(item, prop) in list" :key="prop">
          <span class="budget-commen">{{ item.comment }}</span>
          <span class="budget-value">{{ item.value }}</span>
          <el-button type="danger" @click="deleteItem(item.id)"
            >Delete</el-button
          >
        </div>
      </template>
      <el-alert v-else type="info" :title="emptyTytle" :closable="false" />
    </el-card>
  </div>
</template>

<script>
import { onMounted } from 'vue';
export default {
  name: 'BudgetList',
  props: {
    list: {
      type: Object,
      required: false,
      default: () => ({}),
    },
  },
  emits: ['click'],
  setup(props) {
    let header = 'Budget List';
    let emptyTytle = 'List is empty';
    const isEmpty = () => {
      return Boolean(!Object.keys(props.list).length);
    };

    const deleteItem = (id) => {
      this.$emit('deleteItem', id);
    };

    onMounted(() => {
      console.log();
    });

    return {
      header,
      isEmpty,
      emptyTytle,
      deleteItem,
    };
  },
};
</script>

<style lang="css" scoped>
.list-item {
  display: flex;
  align-items: center;
  padding: 10px 15px;
}

.budget-value {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
}
</style>
