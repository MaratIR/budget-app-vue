<template>
  <ElCard class="form-card">
    <ElForm :model="formData" ref="addItemForm" :rules="rules" label-position="top">
      <ElFormItem label="Type" prop="type">
        <ElSelect class="type-select" v-model="formData.type" placeholder="Choose type...">
          <ElOption label="Income" value="INCOME" />
          <ElOption label="Outcome" value="OUTCOME" />
        </ElSelect>
      </ElFormItem>
      <ElFormItem label="Comemnts" prop="comment">
        <ElInput v-model="formData.comment"/>
      </ElFormItem>
      <ElFormItem label="Value" prop="value">
        <ElInput v-bind:min="[formData.type=='INCOME' ? '1' : '-10000']" v-bind:max="[formData.type=='INCOME' ? '10000' : '-1']" v-model.number="formData.value"/>
      </ElFormItem>
      <ElButton @click="onSubmit" type="primary">Submit</ElButton>
    </ElForm>
  </ElCard>
</template>

<script>
export default {
  name: 'Form',
  data: () => ({
    formData: {
      type: 'INCOME',
      comment: '',
      value: 0,
    },
    rules: {
      type: [
        {
          required: true,
          message: 'Please select type',
          trigger: 'blur'
        },
      ],
      comment: [
        {
          required: true,
          message: 'Please input comment',
          trigger: 'blur'
        },
      ],
      value: [
        {
          required: true,
          message: 'Please input value',
          trigger: 'change'
        },
        {
          type: "number",
          min:1,
          message: 'Value must be a pozitive namber ',
          trigger: 'change'
        },
        // {
        //   valid: true,
        //   message: 'Value must be a pozitive',
        //   trigger: 'change'
        // },
      ],
    },
  }),
  methods: {
    onSubmit() {
      this.$refs.addItemForm.validate((valid) => {
        if (valid) {
          // console.log(...this.formData);
          this.$emit('submitForm', {...this.formData});
          this.$refs.addItemForm.resetFields();
        }
      });
    },
  },
}
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