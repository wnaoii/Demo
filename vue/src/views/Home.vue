<template>
  <div style="padding-right: 10px">
    <!--功能区域-->
    <div style="margin: 10px 0">
      <el-button type="primary" @click="add">新增</el-button>
      <el-button type="primary">导入</el-button>
      <el-button type="primary">导出</el-button>
    </div>
    <!--搜索区域-->
    <div style="margin: 10px 0">
      <el-input v-model="search" placeholder="请输入关键字" style="width: 20%"/>
      <el-button style="margin-left: 5px" type="primary">查询</el-button>
    </div>
    <el-table :data="tableData" border stripe style="width: 100%">
      <el-table-column prop="id" label="ID" sortable />
      <el-table-column prop="username" label="用户名" />
      <el-table-column prop="nickName" label="昵称" />
      <el-table-column prop="age" label="年龄" />
      <el-table-column prop="sex" label="性别" />
      <el-table-column prop="address" label="地址" />
      <el-table-column label="操作">
        <template #default="scope">
          <el-button size="mini" @click="handleEdit(scope.$index,scope.row)">编辑</el-button>
          <el-popconfirm title="确认删除?">
            <template #reference>
              <el-button size="mini" type="danger" @click="handleDelete(scope.$index,scope.row)">删除</el-button>
            </template>
          </el-popconfirm>
        </template>
      </el-table-column>
    </el-table>
    <div >
      <el-pagination
              v-model:currentPage="currentPage"
              :page-sizes="[5, 10, 20]"
              :page-size="pageSize"
              layout="total, sizes, prev, pager, next, jumper"
              :total="total"
              @size-change="handleSizeChange"
              @current-change="handleCurrentChange"
      >
      </el-pagination>

      <el-dialog v-model="dialogVisible" title="提示" width="30%">
        <el-form v-bind:model="form" label-width="120px">
          <!--新增提示弹窗-->
          <el-form-item label="用户名">
            <el-input v-model="form.username" style="width: 80%"></el-input>
          </el-form-item>
          <!--新增提示弹窗-->
          <el-form-item label="昵称">
            <el-input v-model="form.nickName" style="width: 80%"></el-input>
          </el-form-item>
          <!--新增提示弹窗-->
          <el-form-item label="年龄">
            <el-input v-model="form.age" style="width: 80%"></el-input>
          </el-form-item>
          <!--新增提示弹窗-->
          <el-form-item label="性别">
            <el-radio v-model="form.sex" label="男">男</el-radio>
            <el-radio v-model="form.sex" label="女">女</el-radio>
            <el-radio v-model="form.sex" label="扶她">扶她</el-radio>
          </el-form-item>
          <!--新增提示弹窗-->
          <el-form-item label="地址">
            <el-input type="textarea" v-model="form.address" style="width: 80%"></el-input>
          </el-form-item>

        </el-form>
        <template #footer>
          <span class="dialog-footer">
            <el-button @click="dialogVisible = false">取 消</el-button>
            <el-button type="primary" @click="save">确 定</el-button
            >
          </span>
        </template>
      </el-dialog>

    </div>
  </div>
</template>

<script>

import request from "../utils/request";

export default {
  name: 'Home',
  components: {

  },
  data() {
    return {
      form: {},
      // 弹窗默认关闭
      dialogVisible: false,
      search: '',
      currentPage: 1,
      pageSize: 10,
      total: 0,
      tableData: [

      ]
    }
  },
  created() {
    this.load()
  },
  methods: {

    // 数据查询渲染
    load() {
      request.get("/api/user", {
        pageNum: this.currentPage,
        pageSize: this.currentPage,
        search: this.search
      }).then(res => {
        console.log(res)
        this.tableData = res.data.records
      })
    },

    // 添加数据
    add() {
      this.dialogVisible = true
      // 每次打开清空表单域
      this.form = {}
    },
    save() {
      request.post("/api/user", this.form).then(res => {
        console.log(res)
      })
    },
    handleEdit() {

    },
    handleSizeChange() {

    },
    handleCurrentChange() {

    }
  }
}
</script>