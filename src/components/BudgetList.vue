<template>
  <div v-if="isEmpty" class="budget-list-wrap">
    <ElCard :header="header">
      <ElAlert type="info" :title="emptyTitle" :closable="false" />
    </ElCard>
  </div>
</template>

<script>
export default {
  name: "BudgetList",
  props: {
    list: {
      type: Object,
      default: ()=>({}),
    }
  },
  data: () => ({
    header: 'Budget List',
    emptyTitle: "Empty list",
  }),
  computed: {
    isEmpty() {
      return !Object.keys(this.list).length;
    },
  },
}
</script>

<style scoped>
  .budget-list-wrap {
    max-width: 500px;
    margin: auto;
  }
</style>
