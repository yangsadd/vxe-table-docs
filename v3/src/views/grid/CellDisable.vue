<template>
  <div>
    <p class="tip">通过 <table-api-link prop="edit-config"/>.<table-api-link prop="activeMethod"/> 方法来判断单元格是否禁用，禁用后不可编辑</p>

    <vxe-grid v-bind="gridOptions1" @edit-disabled="editDisabledEvent">
      <template #name_edit="{ row }">
        <vxe-input v-model="row.name"></vxe-input>
      </template>
      <template #sex_edit="{ row }">
        <vxe-input v-model="row.sex"></vxe-input>
      </template>
      <template #age_edit="{ row }">
        <vxe-input v-model="row.age"></vxe-input>
      </template>
      <template #address_edit="{ row }">
        <vxe-input v-model="row.address"></vxe-input>
      </template>
    </vxe-grid>

    <p class="demo-code">{{ $t('app.body.button.showCode') }}</p>

    <pre>
      <pre-code class="xml">{{ demoCodes[0] }}</pre-code>
      <pre-code class="javascript">{{ demoCodes[1] }}</pre-code>
    </pre>

    <p class="tip">禁用第二行编辑</p>

    <vxe-grid v-bind="gridOptions2" @edit-disabled="editDisabledEvent">
      <template #name_edit="{ row }">
        <vxe-input v-model="row.name"></vxe-input>
      </template>
      <template #sex_edit="{ row }">
        <vxe-input v-model="row.sex"></vxe-input>
      </template>
      <template #age_edit="{ row }">
        <vxe-input v-model="row.age"></vxe-input>
      </template>
      <template #address_edit="{ row }">
        <vxe-input v-model="row.address"></vxe-input>
      </template>
    </vxe-grid>

    <p class="demo-code">{{ $t('app.body.button.showCode') }}</p>

    <pre>
      <pre-code class="xml">{{ demoCodes[2] }}</pre-code>
      <pre-code class="javascript">{{ demoCodes[3] }}</pre-code>
    </pre>
  </div>
</template>

<script>
export default {
  data () {
    return {
      gridOptions1: {
        border: true,
        showOverflow: true,
        editConfig: {
          trigger: 'click',
          mode: 'cell',
          activeMethod: this.activeCellMethod
        },
        columns: [
          { type: 'seq', width: 50 },
          { field: 'name', title: 'Name', editRender: {}, slots: { edit: 'name_edit' } },
          { field: 'sex', title: 'Sex', editRender: {}, slots: { edit: 'sex_edit' } },
          { field: 'age', title: 'Age', editRender: {}, slots: { edit: 'age_edit' } },
          { field: 'address', title: 'Address', editRender: {}, slots: { edit: 'address_edit' } }
        ],
        data: [
          { id: 10001, name: 'Test1', nickname: 'T1', role: 'Develop', sex: 'Man', age: 28, address: 'Shenzhen' },
          { id: 10002, name: 'Test2', nickname: 'T2', role: 'Test', sex: 'Women', age: 22, address: 'Guangzhou' },
          { id: 10003, name: 'Test3', nickname: 'T3', role: 'PM', sex: 'Man', age: 32, address: 'Shanghai' },
          { id: 10004, name: 'Test4', nickname: 'T4', role: 'Designer', sex: 'Women', age: 23, address: 'Shenzhen' },
          { id: 10005, name: 'Test5', nickname: 'T5', role: 'Develop', sex: 'Women', age: 30, address: 'Shanghai' }
        ]
      },
      gridOptions2: {
        border: true,
        showOverflow: true,
        editConfig: {
          trigger: 'click',
          mode: 'cell',
          activeMethod: this.activeRowMethod
        },
        columns: [
          { type: 'seq', width: 50 },
          { field: 'name', title: 'Name', editRender: {}, slots: { edit: 'name_edit' } },
          { field: 'sex', title: 'Sex', editRender: {}, slots: { edit: 'sex_edit' } },
          { field: 'age', title: 'Age', editRender: {}, slots: { edit: 'age_edit' } },
          { field: 'address', title: 'Address', editRender: {}, slots: { edit: 'address_edit' } }
        ],
        data: [
          { id: 10001, name: 'Test1', nickname: 'T1', role: 'Develop', sex: 'Man', age: 28, address: 'Shenzhen' },
          { id: 10002, name: 'Test2', nickname: 'T2', role: 'Test', sex: 'Women', age: 22, address: 'Guangzhou' },
          { id: 10003, name: 'Test3', nickname: 'T3', role: 'PM', sex: 'Man', age: 32, address: 'Shanghai' },
          { id: 10004, name: 'Test4', nickname: 'T4', role: 'Designer', sex: 'Women', age: 23, address: 'Shenzhen' },
          { id: 10005, name: 'Test5', nickname: 'T5', role: 'Develop', sex: 'Women', age: 30, address: 'Shanghai' }
        ]
      },
      demoCodes: [
        `
        <vxe-grid v-bind="gridOptions1" @edit-disabled="editDisabledEvent">
          <template #name_edit="{ row }">
            <vxe-input v-model="row.name"></vxe-input>
          </template>
          <template #sex_edit="{ row }">
            <vxe-input v-model="row.sex"></vxe-input>
          </template>
          <template #age_edit="{ row }">
            <vxe-input v-model="row.age"></vxe-input>
          </template>
          <template #address_edit="{ row }">
            <vxe-input v-model="row.address"></vxe-input>
          </template>
        </vxe-grid>
        `,
        `
        export default {
          data () {
            return {
              gridOptions1: {
                border: true,
                showOverflow: true,
                editConfig: {
                  trigger: 'click',
                  mode: 'cell',
                  activeMethod: this.activeCellMethod
                },
                columns: [
                  { type: 'seq', width: 50 },
                  { field: 'name', title: 'Name', editRender: {}, slots: { edit: 'name_edit' } },
                  { field: 'sex', title: 'Sex', editRender: {}, slots: { edit: 'sex_edit' } },
                  { field: 'age', title: 'Age', editRender: {}, slots: { edit: 'age_edit' } },
                  { field: 'address', title: 'Address', editRender: {}, slots: { edit: 'address_edit' } }
                ],
                data: [
                  { id: 10001, name: 'Test1', nickname: 'T1', role: 'Develop', sex: 'Man', age: 28, address: 'Shenzhen' },
                  { id: 10002, name: 'Test2', nickname: 'T2', role: 'Test', sex: 'Women', age: 22, address: 'Guangzhou' },
                  { id: 10003, name: 'Test3', nickname: 'T3', role: 'PM', sex: 'Man', age: 32, address: 'Shanghai' },
                  { id: 10004, name: 'Test4', nickname: 'T4', role: 'Designer', sex: 'Women', age: 23, address: 'Shenzhen' },
                  { id: 10005, name: 'Test5', nickname: 'T5', role: 'Develop', sex: 'Women', age: 30, address: 'Shanghai' }
                ]
              }
            }
          },
          methods: {
            activeCellMethod ({ column, columnIndex }) {
              if (columnIndex === 1) {
                return false
              }
              return true
            },
            editDisabledEvent ({ row, column }) {
              console.log('禁止编辑')
            }
          }
        }
        `,
        `
        <vxe-grid v-bind="gridOptions2" @edit-disabled="editDisabledEvent">
          <template #name_edit="{ row }">
            <vxe-input v-model="row.name"></vxe-input>
          </template>
          <template #sex_edit="{ row }">
            <vxe-input v-model="row.sex"></vxe-input>
          </template>
          <template #age_edit="{ row }">
            <vxe-input v-model="row.age"></vxe-input>
          </template>
          <template #address_edit="{ row }">
            <vxe-input v-model="row.address"></vxe-input>
          </template>
        </vxe-grid>
        `,
        `
        export default {
          data () {
            return {
              gridOptions2: {
                border: true,
                showOverflow: true,
                editConfig: {
                  trigger: 'click',
                  mode: 'cell',
                  activeMethod: this.activeRowMethod
                },
                columns: [
                  { type: 'seq', width: 50 },
                  { field: 'name', title: 'Name', editRender: {}, slots: { edit: 'name_edit' } },
                  { field: 'sex', title: 'Sex', editRender: {}, slots: { edit: 'sex_edit' } },
                  { field: 'age', title: 'Age', editRender: {}, slots: { edit: 'age_edit' } },
                  { field: 'address', title: 'Address', editRender: {}, slots: { edit: 'address_edit' } }
                ],
                data: [
                  { id: 10001, name: 'Test1', nickname: 'T1', role: 'Develop', sex: 'Man', age: 28, address: 'Shenzhen' },
                  { id: 10002, name: 'Test2', nickname: 'T2', role: 'Test', sex: 'Women', age: 22, address: 'Guangzhou' },
                  { id: 10003, name: 'Test3', nickname: 'T3', role: 'PM', sex: 'Man', age: 32, address: 'Shanghai' },
                  { id: 10004, name: 'Test4', nickname: 'T4', role: 'Designer', sex: 'Women', age: 23, address: 'Shenzhen' },
                  { id: 10005, name: 'Test5', nickname: 'T5', role: 'Develop', sex: 'Women', age: 30, address: 'Shanghai' }
                ]
              }
            }
          },
          methods: {
            activeRowMethod ({ row, rowIndex }) {
              if (rowIndex === 1) {
                return false
              }
              return true
            },
            editDisabledEvent ({ row, column }) {
              console.log('禁止编辑')
            }
          }
        }
        `
      ]
    }
  },
  methods: {
    activeCellMethod ({ columnIndex }) {
      if (columnIndex === 1) {
        return false
      }
      return true
    },
    activeRowMethod ({ rowIndex }) {
      if (rowIndex === 1) {
        return false
      }
      return true
    },
    editDisabledEvent () {
      console.log('禁止编辑')
    }
  }
}
</script>
