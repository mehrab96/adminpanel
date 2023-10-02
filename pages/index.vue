<script lang="ts" setup>
import {Runtime} from "inspector";
import Timestamp = module

const columns = [
  {
    title: 'title',
    dataIndex: 'title',
    key: 'title',

  },
  {
    title: 'slug',
    dataIndex: 'slug',
    key: 'slug',
    width: '20%',
  },
  {
    title: 'status',
    dataIndex: 'status',
    width: '10%',
    key: 'status',
  },
  {
    title: 'time',
    dataIndex: 'time',
    width: '10%',
    key: 'time',
  },
];

interface DataItem {
  key: number;
  title: String;
  slug: string;
  status: string;
  time: String;
}

const data: DataItem[] = [
  {
    key: 1,
    title: 'John Brown sr.',
    slug: 'John Brown sr.',
    status: 'publish',
    time: '2023',
  },
  {
    key: 2,
    title: 'John Brown sr.',
    slug: 'Joe Black',
    status: 'pending',
    time: '2023',
  },
];

const rowSelection = ref({
  checkStrictly: false,
  onChange: (selectedRowKeys: (string | number)[], selectedRows: DataItem[]) => {
    console.log(`selectedRowKeys: ${selectedRowKeys}`, 'selectedRows: ', selectedRows);
  },
  onSelect: (record: DataItem, selected: boolean, selectedRows: DataItem[]) => {
    console.log(record, selected, selectedRows);
  },
  onSelectAll: (selected: boolean, selectedRows: DataItem[], changeRows: DataItem[]) => {
    console.log(selected, selectedRows, changeRows);
  },
});
definePageMeta({ layout: 'master'});
</script>

<template>
<section>
  <h1>hello nuxt 3</h1>

  <a-table :columns="columns" :data-source="data" :row-selection="rowSelection">
    <template #bodyCell="{ column, record }">
      <template v-if="column.key === 'status'">
        <a-tag v-if="record.status == 'publish'" :color="'green'">
          {{ record.status }}
        </a-tag>
        <a-tag v-else-if="record.status == 'pending'" :color="'orange'">
          {{ record.status }}
        </a-tag>
      </template>
    </template>
  </a-table>
</section>
</template>

