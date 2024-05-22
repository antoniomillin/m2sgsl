<script setup lang="ts">
import DataTable from 'datatables.net-vue3';
import DataTablesCore from 'datatables.net';
import 'datatables.net-buttons';
import 'datatables.net-buttons/js/buttons.html5';
import 'datatables.net-responsive';
import 'datatables.net-select';

DataTable.use(DataTablesCore);

const columns = [
  { data: 'custId' },
  { data: 'custDescr' },
  { data: 'custGUID' },
];

const options = {
  dom: 'Blrtip',
  responsive: true,
  select: true,
  language: {"url": "//cdn.datatables.net/plug-ins/1.10.18/i18n/Italian.json"},
  pageLength: 25,
  pagingType: 'full_numbers',
  lengthMenu: [ [10, 25, 50, 100], [10, 25, 50, 100] ],
  buttons: ['pdf','excel','print'],
  columnDefs:[
  {
    render: function (data:any, type:any, row:any) {
        let mlinkEdit = 'javascript:editRecord(' + data + ')';
        let mlinkDelete = 'javascript:deleteRecord(' + data + ')';
        let szReturn = '<a href="' + mlinkEdit + '"><img src="assets/images/icons/edit.png" width="20"/></a>';
        szReturn += '&nbsp;<a href="' + mlinkDelete + '"><img src="assets/images/icons/delete.png" width="20"/></a>';
        return szReturn;
    },
    width: 50,
    orderable: false,
    className: "text-center noclick",
    targets: 0
  }
  ],
  initComplete: function () {
    alert('bingo');
  }
};
</script>

<template>
  <div>
    <h1>CORSI</h1>
    <h2>DataTables + Vue3 example</h2>
    
    <DataTable
      :columns="columns"
      :options="options"
      ajax="https://m2sgsl-api-b0dec18fded3.herokuapp.com/customer/"
      class="table table-striped table-bordered"
      width="100%"
      id="mTable"
    >
      <thead>
        <tr>
          <th>id</th>
          <th>descr</th>
          <th>guid</th>
        </tr>
      </thead>
      <tfoot>
        <tr>
          <th>id</th>
          <th>descr</th>
          <th>guid</th>
        </tr>
      </tfoot>
    </DataTable>
  </div>
</template>

<style>
@import 'datatables.net-dt';
@import 'datatables.net-buttons-dt';
@import 'datatables.net-responsive-dt';
@import 'datatables.net-select-dt';
</style>
