<template>
  <el-card class="form-card">
    <el-form
      :model="formData"
      ref="addItemForm"
      :rules="rules"
      label-position="top"
    >
      <el-form-item label="Type" prop="type">
        <el-select
          v-model="formData.type"
          placeholder="Choose Type..."
          class="type-select"
        >
          <el-option label="Income" value="INCOME" />
          <el-option label="Outcome" value="OUTCOME" />
        </el-select>
      </el-form-item>
      <el-form-item label="Comments" prop="comment">
        <el-input v-model="formData.comment" />
      </el-form-item>
      <el-form-item label="Value" prop="value">
        <el-input v-model.number="formData.value" />
      </el-form-item>
      <el-button @click="onSubmit" type="primary">Submit</el-button>
    </el-form>
  </el-card>
</template>

<script>
import { ref } from 'vue';
export default {
  emits: ['submitForm'],
  setup(_, { emit }) {
    const formData = ref({
      type: 'INCOME',
      comment: '',
      value: 0,
    });

    let rules = ref({
      type: [
        { required: true, message: 'Please select type', trigger: 'blur' },
      ],
      comment: [
        { required: true, message: 'Please enter comment', trigger: 'blur' },
      ],
      value: [
        { required: true, message: 'Please enter value', trigger: 'change' },
        {
          type: 'number',
          message: 'Please enter only number',
          trigger: 'change',
        },
      ],
    });
    const addItemForm = ref();

    const onSubmit = () => {
      addItemForm.value.validate((valid) => {
        if (valid) {
          emit('submitForm', { ...formData.value });
          addItemForm.value.resetFields();
        }
      });
    };

    return {
      formData,
      onSubmit,
      rules,
      addItemForm,
    };
  },
};
</script>

<style scoped>
.form-card {
  max-width: 500px;
  margin: auto;
}
.type-select {
  width: 100%;
}
</style>
