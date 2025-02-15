<template>
  <div>
    <h1>{{ $t('app.aside.nav.commands') }}</h1>
    <p class="tip">
      将工具栏按钮或数据代理中常用的指令注册成全局可复用<br>
      <span class="red">（注：高级功能难度较高，不适合非前端和初级前端使用）</span>
    </p>
    <vxe-table
      resizable
      :row-config="{isCurrent: true, isHover: true}"
      :column-config="{isCurrent: true}"
      :data="tableData">
      <vxe-column field="name" title="app.api.title.prop" min-width="280" tree-node></vxe-column>
      <vxe-column field="desc" title="app.api.title.desc" min-width="200"></vxe-column>
      <vxe-column field="type" title="app.api.title.type" min-width="140"></vxe-column>
      <vxe-column field="enum" title="app.api.title.enum" min-width="150"></vxe-column>
      <vxe-column field="defVal" title="app.api.title.defVal" min-width="160"></vxe-column>
    </vxe-table>
    <h2>示例</h2>
    <pre>
      <pre-code class="html">{{ demoCodes[0] }}</pre-code>
      <pre-code class="javascript">{{ demoCodes[1] }}</pre-code>
      <pre-code class="html">{{ demoCodes[2] }}</pre-code>
      <pre-code class="javascript">{{ demoCodes[3] }}</pre-code>
    </pre>
  </div>
</template>

<script>
export default {
  data () {
    return {
      tableData: [
        {
          name: 'add(code, callback)',
          desc: '添加一个',
          version: '',
          type: '',
          enum: '',
          defVal: 'code: string, callback: (params) => any',
          list: []
        },
        {
          name: 'mixin(options)',
          desc: '添加多个',
          version: '',
          type: '',
          enum: '',
          defVal: 'options: { [code: string]: (params) => any }',
          list: []
        },
        {
          name: 'delete(code)',
          desc: '删除',
          version: '',
          type: '',
          enum: '',
          defVal: 'code: string',
          list: []
        }
      ],
      demoCodes: [
        `
        <vxe-toolbar :buttons="toolbarButtons"></vxe-toolbar>

        <vxe-table
          border
          :data="tableData">
          <vxe-column type="seq" width="60"></vxe-column>
          <vxe-column field="name" title="Name"></vxe-column>
          <vxe-column field="sex" title="sex"></vxe-column>
          <vxe-column field="age" title="Age"></vxe-column>
        </vxe-table>
        `,
        `
        VXETable.commands.add('exportBtn', (params) => {
          let { $table, code, button } = params
          $table.exportData()
        })

        export default {
          data () {
            return {
              toolbarButtons: [
                {
                  code: 'exportBtn',
                  name: '导出.csv'
                }
              ],
              tableData: [
                { id: 10001, name: 'Test1', role: 'Develop', sex: 'Man', age: 28, address: 'Shenzhen' },
                { id: 10002, name: 'Test2', role: 'Test', sex: 'Women', age: 22, address: 'Guangzhou' },
                { id: 10003, name: 'Test3', role: 'PM', sex: 'Man', age: 32, address: 'Shanghai' },
                { id: 10004, name: 'Test4', role: 'Designer', sex: 'Women', age: 24, address: 'Shanghai' }
              ]
            }
          }
        }
        `,
        `
        <button @click="printEvent">打印</button>
        <vxe-grid
          border
          resizable
          ref="xGrid"
          height="300"
          :columns="tableColumn"
          :data="tableData">
        </vxe-grid>
        `,
        `
        VXETable.commands.add('myPrint', (params) => {
          let { $table, code, button } = params
          $table.print()
        })

        export default {
          data () {
            return {
              tableColumn: [
                { type: 'seq', width: 50 },
                { field: 'name', title: 'Name' },
                { field: 'sex', title: 'Sex' },
                { field: 'address', title: 'Address' }
              ],
              tableData: [
                { id: 10001, name: 'Test1', role: 'Develop', sex: 'Man', age: 28, address: 'Shenzhen' },
                { id: 10002, name: 'Test2', role: 'Test', sex: 'Women', age: 22, address: 'Guangzhou' },
                { id: 10003, name: 'Test3', role: 'PM', sex: 'Man', age: 32, address: 'Shanghai' },
                { id: 10004, name: 'Test4', role: 'Designer', sex: 'Women', age: 24, address: 'Shanghai' }
              ]
            }
          },
          methods: {
            printEvent () {
              this.$refs.xGrid.commitProxy('myPrint')
            }
          }
        }
        `
      ]
    }
  }
}
</script>
