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
      <el-button type="primary" @click="handleAdd">添加</el-button>
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
      <el-table-column fixed prop="date" label="Date" width="150" />
      <el-table-column prop="name" label="Name" width="120" />
      <el-table-column prop="state" label="State" width="120" />
      <el-table-column prop="city" label="City" width="120" />
      <el-table-column prop="address" label="Address" width="600" />
      <el-table-column prop="zip" label="Zip" width="120" />
      <el-table-column fixed="right" label="Operations" width="120">
        <template #default>
          <el-button
            link
            type="primary"
            size="small"
            @click="handleClick"
            style="color: red"
            >删除</el-button
          >
          <el-button link type="primary" size="small">添加</el-button>
        </template>
      </el-table-column>
    </el-table>

    <!-- dialog -->
    <el-dialog v-model="dialogFormVisible" title="添加信息">
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
          <el-button type="primary" @click="dialogFormVisible = false">
            确认
          </el-button>
        </span>
      </template>
    </el-dialog>
  </div>
</template>

<script setup>
import { ref } from "vue";

// 数据
let queryInput = ref("");
let tableData = ref([
  {
    date: "2016-05-03",
    name: "Tom",
    state: "California",
    city: "Los Angeles",
    address: "No. 189, Grove St, Los Angeles",
    zip: "CA 90036",
    tag: "Home",
  },
  {
    date: "2016-05-02",
    name: "Tom",
    state: "California",
    city: "Los Angeles",
    address: "No. 189, Grove St, Los Angeles",
    zip: "CA 90036",
    tag: "Office",
  },
  {
    date: "2016-05-04",
    name: "Tom",
    state: "California",
    city: "Los Angeles",
    address: "No. 189, Grove St, Los Angeles",
    zip: "CA 90036",
    tag: "Home",
  },
  {
    date: "2016-05-01",
    name: "Tom",
    state: "California",
    city: "Los Angeles",
    address: "No. 189, Grove St, Los Angeles",
    zip: "CA 90036",
    tag: "Office",
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

//方法
let handleClick = () => {
  console.log("llll");
};

//多选
const handleSelectionChange = (val) => {
  multipleSelection.value = val;
  console.log(val);
};

//
let handleAdd = () => {
  dialogFormVisible.value = true;
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
