<template>
  <div>
    <vxe-toolbar>
      <template #buttons>
        <vxe-button icon="vxe-icon-square-plus" @click="insertEvent()">新增</vxe-button>
      </template>
    </vxe-toolbar>

    <vxe-table
      border
      show-overflow
      ref="xTable"
      height="300"
      :column-config="{resizable: true}"
      :row-config="{isHover: true}"
      :data="demo1.tableData"
      @cell-dblclick="cellDBLClickEvent">
      <vxe-column type="seq" width="60"></vxe-column>
      <vxe-column field="name" title="Name"></vxe-column>
      <vxe-column field="sex" title="Sex" :formatter="formatterSex"></vxe-column>
      <vxe-column field="age" title="Age"></vxe-column>
      <vxe-column field="address" title="Address" show-overflow></vxe-column>
      <vxe-column title="操作" width="100" show-overflow>
        <template #default="{ row }">
          <vxe-button type="text" icon="vxe-icon-edit" @click="editEvent(row)"></vxe-button>
          <vxe-button type="text" icon="vxe-icon-delete" @click="removeEvent(row)"></vxe-button>
        </template>
      </vxe-column>
    </vxe-table>

    <vxe-modal v-model="demo1.showEdit" :title="demo1.selectRow ? '编辑&保存' : '新增&保存'" width="800" min-width="600" min-height="300" :loading="demo1.submitLoading" resize destroy-on-close>
      <template #default>
        <vxe-form :data="demo1.formData" :rules="demo1.formRules" title-align="right" title-width="100" @submit="submitEvent">
          <vxe-form-item title="Basic information" title-align="left" :title-width="200" :span="24" :title-prefix="{icon: 'vxe-icon-comment'}"></vxe-form-item>
          <vxe-form-item field="name" title="Name" :span="12" :item-render="{}">
            <template #default="{ data }">
              <vxe-input v-model="data.name" placeholder="请输入名称"></vxe-input>
            </template>
          </vxe-form-item>
          <vxe-form-item field="nickname" title="Nickname" :span="12" :item-render="{}">
            <template #default="{ data }">
              <vxe-input v-model="data.name" placeholder="请输入名称"></vxe-input>
            </template>
          </vxe-form-item>
          <vxe-form-item field="role" title="Role" :span="12" :item-render="{}">
            <template #default="{ data }">
              <vxe-input v-model="data.name" placeholder="请输入角色"></vxe-input>
            </template>
          </vxe-form-item>
          <vxe-form-item field="sex" title="Sex" :span="12" :item-render="{}">
            <template #default="{ data }">
              <vxe-select v-model="data.sex" transfer>
                <vxe-option v-for="item in demo1.sexList" :key="item.value" :value="item.value" :label="item.label"></vxe-option>
              </vxe-select>
            </template>
          </vxe-form-item>
          <vxe-form-item field="age" title="Age" :span="12" :item-render="{}">
            <template #default="{ data }">
              <vxe-input v-model="data.age" type="number" placeholder="请输入年龄"></vxe-input>
            </template>
          </vxe-form-item>
          <vxe-form-item field="flag1" title="是否单身" :span="12" :item-render="{}">
            <template #default="{ data }">
              <vxe-radio-group v-model="data.flag1">
                <vxe-radio label="Y" content="是"></vxe-radio>
                <vxe-radio label="N" content="否"></vxe-radio>
              </vxe-radio-group>
            </template>
          </vxe-form-item>
          <vxe-form-item field="checkedList" title="可选信息" :visible-method="visibleMethod" :span="24" :item-render="{}">
            <template #default="{ data }">
              <vxe-checkbox-group v-model="data.checkedList">
                <vxe-checkbox label="1" content="运动、跑步"></vxe-checkbox>
                <vxe-checkbox label="2" content="听音乐"></vxe-checkbox>
                <vxe-checkbox label="3" content="爬山"></vxe-checkbox>
                <vxe-checkbox label="4" content="吃美食"></vxe-checkbox>
              </vxe-checkbox-group>
            </template>
          </vxe-form-item>
          <vxe-form-item title="Other information" title-align="left" :title-width="200" :span="24" :title-prefix="{message: '请填写必填项', icon: 'vxe-icon-info-circle-fill'}"></vxe-form-item>
          <vxe-form-item field="num" title="Number" :span="12" :item-render="{}">
            <template #default="{ data }">
              <vxe-input v-model="data.num" type="number" placeholder="请输入数值"></vxe-input>
            </template>
          </vxe-form-item>
          <vxe-form-item field="date3" title="Date" :span="12" :item-render="{}">
            <template #default="{ data }">
              <vxe-input v-model="data.date3" type="date" placeholder="请选择日期" transfer></vxe-input>
            </template>
          </vxe-form-item>
          <vxe-form-item field="address" title="Date" :span="24" :item-render="{}" :title-suffix="{message: '提示信息！！', icon: 'vxe-icon-question-circle-fill'}">
            <template #default="{ data }">
              <vxe-textarea v-model="data.address" :autosize="{minRows: 2, maxRows: 4}"></vxe-textarea>
            </template>
          </vxe-form-item>
          <vxe-form-item align="center" title-align="left" :span="24">
            <template #default>
              <vxe-button type="submit">提交</vxe-button>
              <vxe-button type="reset">重置</vxe-button>
            </template>
          </vxe-form-item>
        </vxe-form>
      </template>
    </vxe-modal>
  </div>
</template>

<script lang="ts" setup>
import { reactive, ref } from 'vue'
import { VXETable, VxeTableInstance, VxeColumnPropTypes, VxeFormPropTypes, VxeFormItemPropTypes, VxeTableEvents } from 'vxe-table'

interface RowVO {
  id: number
  name: string
  nickname: string
  role: string
  sex: string
  sex2: string[]
  num: number
  num1: number
  age: number
  flag1: boolean
  address: string
  date12: string
  date13: string
  date3: string
  checkedList: any[]
}

const demo1 = reactive({
  submitLoading: false,
  tableData: [] as RowVO[],
  selectRow: null as RowVO | null,
  showEdit: false,
  formData: {
    name: '',
    nickname: '',
    role: '',
    sex: '',
    age: 0,
    num: 0,
    checkedList: [] as any[],
    flag1: false,
    date3: '',
    address: ''
  },
  sexList: [
    { label: '女', value: '0' },
    { label: '男', value: '1' }
  ],
  formRules: {
    name: [
      { required: true, message: '请输入名称' },
      { min: 3, max: 5, message: '长度在 3 到 5 个字符' }
    ],
    nickname: [
      { required: true, message: '请输入昵称' }
    ],
    sex: [
      { required: true, message: '请选择性别' }
    ]
  } as VxeFormPropTypes.Rules
})

const xTable = ref<VxeTableInstance>()

const formatterSex: VxeColumnPropTypes.Formatter = ({ cellValue }) => {
  const item = demo1.sexList.find(item => item.value === cellValue)
  return item ? item.label : ''
}

const visibleMethod: VxeFormItemPropTypes.VisibleMethod = ({ data }) => {
  return data.flag1 === 'Y'
}

const insertEvent = () => {
  demo1.formData = {
    name: '',
    nickname: '',
    role: '',
    sex: '',
    age: 0,
    num: 0,
    checkedList: [],
    flag1: false,
    date3: '',
    address: ''
  }
  demo1.selectRow = null
  demo1.showEdit = true
}

const editEvent = (row: RowVO) => {
  demo1.formData = {
    name: row.name,
    nickname: row.nickname,
    role: row.role,
    sex: row.sex,
    age: row.age,
    num: row.num,
    checkedList: row.checkedList,
    flag1: row.flag1,
    date3: row.date3,
    address: row.address
  }
  demo1.selectRow = row
  demo1.showEdit = true
}

const cellDBLClickEvent: VxeTableEvents.CellDblclick = ({ row }) => {
  editEvent(row)
}

const removeEvent = async (row: any) => {
  const type = await VXETable.modal.confirm('您确定要删除该数据?')
  if (type === 'confirm') {
    const $table = xTable.value
    if ($table) {
      $table.remove(row)
    }
  }
}

const submitEvent = () => {
  demo1.submitLoading = true
  setTimeout(() => {
    const $table = xTable.value
    if ($table) {
      demo1.submitLoading = false
      demo1.showEdit = false
      if (demo1.selectRow) {
        VXETable.modal.message({ content: '保存成功', status: 'success' })
        Object.assign(demo1.selectRow, demo1.formData)
      } else {
        VXETable.modal.message({ content: '新增成功', status: 'success' })
        $table.insert(demo1.formData)
      }
    }
  }, 500)
}

setTimeout(() => {
  const list = [
    { id: 10001, name: 'Test1', nickname: 'T1', role: 'Develop', sex: '0', sex2: ['0'], num: 40, num1: 40, age: 28, flag1: false, address: 'Shenzhen', date3: '', date12: '', date13: '', checkedList: [] },
    { id: 10002, name: 'Test2', nickname: 'T2', role: 'Designer', sex: '1', sex2: ['0', '1'], num: 40, num1: 20, age: 22, flag1: false, address: 'Guangzhou', date3: '', date12: '', date13: '2020-08-20', checkedList: [] },
    { id: 10003, name: 'Test3', nickname: 'T3', role: 'Test', sex: '0', sex2: ['1'], num: 4, num1: 200, age: 32, flag1: true, address: 'Shanghai', date3: '', date12: '2020-09-10', date13: '', checkedList: [] },
    { id: 10004, name: 'Test4', nickname: 'T4', role: 'Designer', sex: '1', sex2: ['0'], num: 3, num1: 30, age: 23, flag1: false, address: 'Shenzhen', date3: '', date12: '', date13: '2020-12-04', checkedList: [] },
    { id: 10004, name: 'Test5', nickname: 'T5', role: 'Designer', sex: '1', sex2: ['1'], num: 40, num1: 30, age: 26, flag1: true, address: 'Shenzhen', date3: '', date12: '', date13: '', checkedList: [] },
    { id: 10004, name: 'Test6', nickname: 'T6', role: 'Designer', sex: '1', sex2: ['1'], num: 5, num1: 30, age: 28, flag1: false, address: 'BeiJing', date3: '', date12: '', date13: '2020-09-04', checkedList: [] },
    { id: 10004, name: 'Test7', nickname: 'T7', role: 'Designer', sex: '1', sex2: ['1'], num: 40, num1: 30, age: 30, flag1: false, address: 'BeiJing', date3: '', date12: '', date13: '2020-04-10', checkedList: [] }
  ]
  demo1.tableData = list
}, 100)
</script>
