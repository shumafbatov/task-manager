<template>
  <el-table
      ref="multipleTable"
      :data="tableData"
      style="width: 100%"
      @selection-change="handleSelectionChange"
  >
    <el-table-column
        type="selection"
        width="55"
    >
    </el-table-column>
    <el-table-column
        label="Date"
        width="120"
    >
      <template #default="scope">{{ scope.row.date }}</template>
    </el-table-column>
    <el-table-column
        property="name"
        label="Name"
        width="120"
    >
    </el-table-column>
    <el-table-column
        property="address"
        label="Address"
        show-overflow-tooltip
    >
    </el-table-column>
  </el-table>

  <div style="margin-top: 20px">
    <el-button @click="toggleSelection([tableData[1], tableData[2]])">
      Toggle selection status of second and third rows
    </el-button>
    <el-button @click="toggleSelection()">
      Clear selection
    </el-button>
  </div>
</template>

<script lang="ts" setup>
import {TASKS} from "@/pages/constants";
import ElTable from "element-plus/es/components/table";

const tableData = ref(TASKS);
const multipleSelection = ref<any[]>([]);
const multipleTable = ref<InstanceType<typeof ElTable> | null>(null);

function toggleSelection(rows: any[] = []) {
  if (rows.length > 0 && multipleTable.value) {
    rows.forEach(row => {
      multipleTable.value.toggleRowSelection(row);
    });
  } else {
    multipleTable.value?.clearSelection();
  }
}

function handleSelectionChange(val: unknown) {
  multipleSelection.value = val as any[];
}
</script>
