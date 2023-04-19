<template>
  <div class="table-box">
    <div>
      <!-- 标题 -->
      <div class="title">
        <h2>CRUD DEMO</h2>
      </div>
    </div>
    <!-- query-box -->
    <div class="query-box">
      <el-input
        class="query-input"
        v-model="queryInput"
        placeholder="请输入姓名搜索"
      ></el-input>
      <div class="button-list">
        <el-button
          type="primary"
          @click="handleDelAll"
          style="background-color: red"
          v-if="multipleSelection.length > 0"
          >全部删除</el-button
        >
        <el-button type="primary" @click="handleAdd">添加</el-button>
      </div>
    </div>

    <!-- table -->
    <el-table
      ref="multipleTableRef"
      :data="tableData"
      style="width: 100%"
      @selection-change="handleSelectionChange"
      border
    >
      <el-table-column type="selection" width="55" />
      <el-table-column prop="name" label="姓名" width="120" />
      <el-table-column prop="email" label="邮箱" width="120" />
      <el-table-column prop="phone" label="电话" width="120" />
      <el-table-column prop="state" label="状态" width="120" />
      <el-table-column prop="add" label="地址" width="210" />
      <el-table-column fixed="right" label="操作" width="120">
        <template #default="scope">
          <el-button
            link
            type="primary"
            size="small"
            @click="handleClickDel(scope.row)"
            style="color: red"
            >删除</el-button
          >
          <el-button
            link
            type="primary"
            size="small"
            @click="handleEdit(scope.row)"
            >编辑</el-button
          >
        </template>
      </el-table-column>
    </el-table>

    <!-- dialog -->
    <el-dialog
      v-model="dialogFormVisible"
      :title="dialogType === 'add' ? '添加信息' : '修改信息'"
    >
      <el-form :model="form">
        <el-form-item label="姓名" :label-width="80">
          <el-input v-model="tableForm.name" autocomplete="off" />
        </el-form-item>
        <el-form-item label="邮箱" :label-width="80">
          <el-input v-model="tableForm.email" autocomplete="off" />
        </el-form-item>
        <el-form-item label="电话" :label-width="80">
          <el-input v-model="tableForm.phone" autocomplete="off" />
        </el-form-item>
        <el-form-item label="状态" :label-width="80">
          <el-input v-model="tableForm.state" autocomplete="off" />
        </el-form-item>
        <el-form-item label="地址" :label-width="80">
          <el-input v-model="tableForm.add" autocomplete="off" />
        </el-form-item>
      </el-form>

      <template #footer>
        <span class="dialog-footer">
          <el-button type="primary" @click="dialogConfirm"> 确认 </el-button>
        </span>
      </template>
    </el-dialog>
  </div>
</template>

<script setup>
import { Loading } from "element-plus/es/components/loading/src/service";
import { ref } from "vue";

// 数据
let queryInput = ref("");

let tableData = ref([
  {
    id: "1",
    name: "Tom",
    email: "123@gamil.com",
    phone: "122332",
    state: "家里蹲",
    add: "北京",
  },
  {
    id: "2",
    name: "Kimi",
    email: "123@gamil.com",
    phone: "122332",
    state: "上学",
    add: "天津",
  },
  {
    id: "3",
    name: "Jenny",
    email: "123@gamil.com",
    phone: "122332",
    state: "打工人",
    add: "上海",
  },
  {
    id: "4",
    name: "Whate",
    email: "123@gamil.com",
    phone: "122332",
    state: "刚出生",
    add: "河北",
  },
]);
let multipleSelection = ref([]);
let dialogFormVisible = ref(false);
let tableForm = ref({
  name: "小明",
  email: "122@gmail.com",
  phone: "999-885",
  state: "在职",
  add: "北京",
});
let dialogType = ref("add");

/**方法 */
//修改
let handleEdit = (row) => {
  dialogFormVisible.value = true;
  dialogType = "edit";
  tableForm.value = { ...row };
};

//单条删除
let handleClickDel = ({ id }) => {
  let index = tableData.value.findIndex((item) => item.id === id);
  tableData.value.splice(index, 1);
};
//多选删除
let handleDelAll = () => {
  multipleSelection.forEach((id) => {
    handleClickDel({ id });
  });
};
//多选
const handleSelectionChange = (val) => {
  multipleSelection = [];
  val.forEach((item) => {
    multipleSelection.push(item.id);
  });
};

//添加
let handleAdd = () => {
  dialogFormVisible.value = true;
  tableForm.value = {};
  dialogType = "add";
};
let dialogConfirm = () => {
  dialogFormVisible.value = false;

  if (dialogType === "add") {
    //添加到title
    tableData.value.push({
      id: (tableData.value.length + 1).toString(),
      ...tableForm.value,
    });
  } else {
    //1.获取当前这条数据索引值
    let index = tableData.value.findIndex(
      (item) => item.id === tableForm.value.id
    );

    //2.替换当前索引对应的数据
    tableData.value[index] = tableForm.value;
  }
};
</script>

<style scoped>
.table-box {
  width: 800px;
  margin: 200px auto;
}
.title {
  text-align: center;
}

.query-box {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

.query-input {
  width: 200px;
}
</style>
