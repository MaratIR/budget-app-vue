<template>
  <div id="app">
    <Form @submitForm="onFormSubmit"/>
    <TotalBalance :total="totalBalance"/>
    <BudgetList :list="list" />
    <BudgetListItem :list="list" @deleteItem="onDeleteItem"/>
  </div>
</template>

<script>
import BudgetList from '@/components/BudgetList';
import TotalBalance from '@/components/TotalBalance.vue';
import Form from '@/components/Form.vue';
import BudgetListItem from './components/BudgetListItem.vue';

export default {
  name: 'app',
  components: {
    BudgetList,
    TotalBalance,
    Form,
    BudgetListItem,
   },
  data: () => ({
    list: {
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
    },
  }),
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce(
        (acc, item) => acc + item.value,
        // (acc, item) => {
        //   if (item.type=='INCOME') {
        //     acc + item.value
        //   } else {
        //     acc + (-item.value)
        //   }
        // }
        0
      );
    },
  },
  methods: {
    onDeleteItem(id) {
      console.log('confirm second', id);
      this.$delete(this.list, id);
    },
    onFormSubmit(data) {
      const newObj = {
        // ...data,
        type: data.type,
        comment: data.comment,
        id: String(Math.random()),
        value: data.value,
      };
      if (newObj.type!='INCOME') {
        newObj.value=-1*newObj.value
      }
      this.$set(this.list, newObj.id, newObj);
      console.log(newObj);
    },
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
