<template>
  <div class="hello">
    <el-table @selection-change="selectChange" border :data="dataList">
      <el-table-column
        :resizable="false"
        min-width="30px"
        :render-header="renderHeader"
        align="center"
      >
        <template slot-scope="scope">
          <el-checkbox
            v-model="scope.row.itemCheck"
            @change="toggleCheck(scope.row)"
            :disabled="disableCheckout(scope.row)"
            :checked="checked(scope.row)"
          ></el-checkbox>
        </template>
      </el-table-column>

      <el-table-column prop="name" show-overflow-tooltip label="名称">
      </el-table-column>
      <el-table-column prop="age" show-overflow-tooltip label="名称">
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
const cityOptions = ['上海', '北京', '广州', '深圳']
export default {
  data() {
    return {
      checkAll: false,
      checkedCities: ['上海', '北京'],
      cities: cityOptions,
      isIndeterminate: true,
      //------------------
      dataList: [
        { id: 0, name: '0333', age: 12, itemCheck: false },
        { id: 1, name: '1333', age: 12, itemCheck: false },
        { id: 2, name: '2333', age: 12, itemCheck: false },
        { id: 3, name: '3333', age: 12, itemCheck: false },
        { id: 4, name: '4333', age: 12, itemCheck: false },
        { id: 5, name: '5333', age: 12, itemCheck: false }
      ],
      isCheck: false,
      indeterminate: false,
      checkedCount: 0,
      selection: []
    }
  },
  methods: {
    checked(row) {
      if (row.id === 4) {
        row.checked = true
        return true
      }
    },
    selectChange(selected) {
      console.log(selected)
    },
    renderHeader(h) {
      return h('span', [
        h('el-checkbox', {
          on: {
            change: this.selectBox
          },
          props: {
            value: this.isCheck,
            indeterminate: this.indeterminate
          }
        })
      ])
    },
    selectBox() {
      this.isCheck = !this.isCheck
      let list = [...this.dataList]
      console.log('list', list)
      for (let val of list) {
        val.itemCheck = this.isCheck
      }
      this.dataList = list
    },
    toggleCheck(row) {
      // 获取已勾选
      let list = this.dataList.filter((item) => item.itemCheck)
      this.isCheck = list.length === this.dataList.length
      this.indeterminate = list.length > 0 && list.length < this.dataList.length
      console.log(this.indeterminate, row)
    },
    disableCheckout(row) {
      // console.log('row', row)
      return row.id === 4
    }
  },
  watch: {}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
