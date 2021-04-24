<template>
  <div v-if="!isEmpty" class="budget-list-wrap">
    <ElCard :header="header">
      <ElButton type="default" size="mini" @click=" listType = '' ">
            All
      </ElButton>
      <ElButton type="success" size="mini" class="el-icon-top" @click=" listType = 'INCOME' ">
            Income
      </ElButton>
      <ElButton type="danger" size="mini" class="el-icon-bottom" @click=" listType = 'OUTCOME' ">
            Outcome
      </ElButton>
      <template>
        <div v-for="(item, prop) in list" :key="prop">
          <div v-if=" item.type==listType || listType==''" class="list-item"
            v-bind:class="[item.type=='INCOME' ? 'el-icon-top' : 'el-icon-bottom' ]"
          >
            <span class="budget-comment">{{ item.comment }}</span>
            <span v-bind:class="[item.value>0 ? 'green' : 'red' ]" class="budget-value">{{ item.value }}</span>
            <!-- <ElButton type="danger" size="mini" @click="deleteItem(item.id)">
             Delete
            </ElButton> -->
            <ElButton type="danger" size="mini" @click="dialogVisible=true">
              Delete
            </ElButton>
            <ElDialog
              title="Danger"
              :visible.sync="dialogVisible"
              width="30%"
              :before-close="deleteItem">
              <span>Are you sure to delete this item?</span>
              <span slot="footer" class="dialog-footer">
                <el-button @click="dialogVisible = false">Cancel</el-button>
                <el-button type="primary" @click="deleteItem(item.id)">Confirm</el-button>
              </span>
            </ElDialog>
          </div>
        </div>
      </template>
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
    },
  },
  data: () => ({
    header: 'Budget List',
    dialogVisible: false,
    listType: '',
  }),
  computed: {
    filteredList: function () {
      return this.list.filter(function (list) {
        return list.type === 'INCOME'
      });
    },
    isEmpty() {
      return !Object.keys(this.list).length;
    },
  },
  methods: {
    deleteItem(id) {
      this.$emit('deleteItem', id);
      this.dialogVisible=false;
      console.log('confirm first',id);
    },
    // handleClose(done) {
    //     this.$confirm('Are you sure to close this dialog?')
    //       .then(() => {done();})
    //       .catch(() => {});
    //   }
  },
}
</script>

<style scoped>
  .budget-list-wrap {
    max-width: 500px;
    margin: auto;
  }

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

  .green {
    color:green;
  }

  .red {
    color: red;
  }

</style>
