<template>
  <div>
    <el-card>
 <!--     <div style="margin-bottom: 20px;">
        <el-button type="danger" size="small" @selection-change="handleSelectionChange">全选</el-button>
        <el-button type="danger" size="small" @click="toggleSelection()">取消全选</el-button>
        <el-button type="danger" size="small" @click="add">删除</el-button>
      </div> -->
      <el-table :data="singlePages" border style="width: 100%" header-align="center">
       <!-- <el-table-column type="selection" width="55">
        </el-table-column> -->
        <el-table-column prop="index" label="ID" width="180" align="center" type="index">
        </el-table-column>
        <el-table-column prop="title" label="用户名" width="180" align="center">
        </el-table-column>
        <el-table-column prop="content" label="留言内容" align="center">
        </el-table-column>
        <el-table-column prop="time" label="留言时间" width="180" align="center">
        </el-table-column>
        <el-table-column label="操作" align="center" width="250">
          <template slot-scope="scope">
            <!-- <el-button size="mini" type="primary" @click="handleEdit(scope.$index, scope.row)">编辑</el-button> -->
            <el-button size="mini" type="danger" @click="handleDelete(scope.$index, scope.row)">删除</el-button>
          </template>
        </el-table-column>
      </el-table>
    </el-card>
    <!-- <el-dialog title="新增单页" :visible.sync="addPage" width="600px" center>
      <el-form status-icon label-width="100px" :model="ruleForm" :rules="rules" ref="ruleForm">
        <el-form-item label="单页模块名" prop="name">
          <el-input type="text" maxlength="10" v-model="ruleForm.name" show-word-limit placeholder="请输入模块名"></el-input>
        </el-form-item>
        <el-form-item label="详细内容" prop="cont">
          <el-input type="textarea" rows="5" maxlength="100" v-model="ruleForm.cont" show-word-limit placeholder="请输入内容"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="addData('ruleForm')" v-if="bt">立即新增</el-button>
          <el-button type="primary" @click="changeData('ruleForm')" v-if="!bt">立即修改</el-button>
        </el-form-item>
      </el-form>
    </el-dialog> -->
  </div>
</template>

<script>
  export default {
    data() {
      return {
        bt: true,
        id: 0,
        ruleForm: {
          name: '',
          cont: ''
        },
        rules: {
          name: [{
            required: true,
            message: '请输入用户名',
            trigger: 'blur'
          }],
          cont: [{
            required: true,
            message: '请输入用户名',
            trigger: 'blur'
          }]
        },
        singlePages: [{
            title: '张三',
            content: '寻求合作机会',
            time: '2017-09-19'
          },
          {
            title: '李四',
            content: '吃饭了没',
            time: '2017-09-19'
          },
          {
            title: '小米',
            content: '我最强',
            time: '2017-09-19'
          },
          {
            title: '小明',
            content: '我好无辜',
            time: '2017-09-19'
          },
          {
            title: '王五',
            content: '就是你',
            time: '2017-09-19'
          }
        ],
        addPage: false,
        multipleSelection: []
      }
    },
    methods: {
      index(index) {
        return index++
      },
      add() {
        this.bt = true
        this.addPage = true
        this.ruleForm = {}
      },
      // 新增
      addData(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            this.singlePages.push({
              title: this.ruleForm.name,
              content: this.ruleForm.cont
            })
            this.addPage = false
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      // 修改
      changeData(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            this.singlePages[this.id].title = this.ruleForm.name
            this.singlePages[this.id].content = this.ruleForm.cont
            this.addPage = false
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      //编辑
      handleEdit(index, row) {
        this.bt = false
        this.addPage = true
        this.ruleForm.name = row.title
        this.ruleForm.cont = row.content
        this.id = index
      },
      // 删除
      handleDelete(index, row) {
        this.singlePages.splice(index, 1)
      },
    }

  }
</script>
<style>
  .el-table {
    margin: auto;
  }
</style>
