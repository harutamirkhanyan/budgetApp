<template>
  <div class="budget-list-wrap">
    <el-card class="box-card" :header="header">
      <template v-if="!isEmpty()">
        <div class="list-item" v-for="(item, prop) in list" :key="prop">
          <span class="budget-commen">{{ item.comment }}</span>
          <span class="budget-value">{{ item.value }}</span>
          <el-button type="danger" @click="$emit('deleteItem', item.id, list)"
            >Delete</el-button
          >
        </div>
      </template>
      <el-alert v-else type="info" :title="emptyTytle" :closable="false" />
    </el-card>
  </div>
</template>

<script>
import { onMounted, ref } from 'vue';
export default {
  name: 'BudgetList',
  props: {
    list: {
      type: Object,
      required: false,
      default: () => ({}),
    },
  },
  emits: ['deleteItem'],
  setup(props) {
    let header = ref('Budget List');
    let emptyTytle = ref('List is empty')
    const isEmpty = () => {
      return Boolean(!Object.keys(props.list).length);
    };

    onMounted(() => {});

    return {
      header,
      isEmpty,
      emptyTytle,
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
