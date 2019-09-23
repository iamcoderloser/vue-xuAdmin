<template>
    <div>
      <el-table
        border
        :data="tableData"
        style="width: 100%">
        <el-table-column
          type="index">
        </el-table-column>
        <el-table-column
          sortable
          prop="user_name"
          label="姓名">
        </el-table-column>
        <el-table-column
          prop="nike_name"
          label="昵称">
        </el-table-column>
        <el-table-column
          prop="gender"
          label="性别">
        </el-table-column>
        <el-table-column
          prop="telephone"
          label="电话"
          width="130">
        </el-table-column>
        <el-table-column
          prop="email"
          label="邮箱">
        </el-table-column>
        
        <el-table-column
          prop="role_name"
          label="角色"
          width="150"
          :filters="[{ text: '职工', value: '职工' }]"
          :filter-method="filterTag"
          filter-placement="bottom-end">
          <template slot-scope="scope">
            <el-tag
              :type="scope.row.role_name === '职工' ? 'primary' : 'success'"
              disable-transitions>{{scope.row.role_name}}</el-tag>
          </template>
        </el-table-column>
        <el-table-column label="操作">
          <template slot-scope="scope">
            <el-button
              size="mini"
              @click="handleEdit(scope.$index, scope.row)">详情</el-button>
            <el-button
              size="mini"
              type="danger"
              @click="handleDelete(scope.$index, scope.row)">删除</el-button>
          </template>
        </el-table-column>
      </el-table>
    </div>
</template>

<script>
export default {
  name: 'maintable',
  data () {
    return {
      tableData: [
    //       {
    //     odd: '201801012345601',
    //     name: '王小虎',
    //     status: '已付款',
    //     amount: '580元',
    //     date: '2018-01-01',
    //     tag: '虚拟'
    //   }
        { user_name: '张三丰',
        nike_name: '牛鼻子',
        gender: '男',
        telephone: '13411122233',
        email: '336603322@qq.com',
        role_name:'职工'
      }]
    }
  },
  methods: {
    handleEdit (index, row) {
      console.log(index, row)
      this.$message({
        showClose: true,
        message: index, row,
        type: 'success'
      })
    },
    handleDelete (index, row) {
      console.log(index, row)
      this.$message({
        showClose: true,
        message: index, row,
        type: 'success'
      })
    },
    formatter (row, column) {
      return row.address
    },
    filterTag (value, row) {
      return row.tag === value
    },
    filterHandler (value, row, column) {
      const property = column['property']
      return row[property] === value
    }
  }
}
</script>

<style scoped>

</style>
