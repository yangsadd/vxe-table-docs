<template>
  <div>
    <h1>{{ $t('app.aside.nav.formats') }}</h1>
    <p class="tip">
      将列的格式化函数注册成全局可复用，通过 <table-column-api-link prop="formatter"/> 调用<br>
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
    </pre>
  </div>
</template>

<script>
export default {
  data () {
    return {
      tableData: [
        {
          name: 'add(name, callback)',
          desc: '添加一个',
          version: '',
          type: '',
          enum: '',
          defVal: 'name: string, callback: (params) => string | number',
          list: []
        },
        {
          name: 'mixin(options)',
          desc: '添加多个',
          version: '',
          type: '',
          enum: '',
          defVal: 'options: { [name: string]: (params) => string | number }',
          list: []
        },
        {
          name: 'delete(name)',
          desc: '删除',
          version: '',
          type: '',
          enum: '',
          defVal: 'name',
          list: []
        }
      ],
      demoCodes: [
        `
        <vxe-table
          border
          :data="tableData">
          <vxe-column type="seq" width="60"></vxe-column>
          <vxe-column field="name" title="Name"></vxe-column>
          <vxe-column field="num1" title="默认两位小数" formatter="myAmount"></vxe-column>
          <vxe-column field="num2" title="保留3位小数" :formatter="['myAmount', 3]"></vxe-column>
        </vxe-table>
        `,
        `
        import XEUtils from 'xe-utils'
        import VXETable from 'vxe-table'

        // 格式金额，默认2位数
        VXETable.formats.add('myAmount', ({ cellValue }, digits = 2) => {
          return XEUtils.commafy(XEUtils.toNumber(cellValue), { digits })
        })

        export default {
          data () {
            return {
              tableData: [
                { id: 10001, name: 'Test1', role: 'Develop', num2: 22, num1: 28, address: 'Shenzhen' },
                { id: 10002, name: 'Test2', role: 'Test', num2: 10, num1: 22, address: 'Guangzhou' },
                { id: 10003, name: 'Test3', role: 'PM', num2: 5, num1: 32, address: 'Shanghai' },
                { id: 10004, name: 'Test4', role: 'Designer', num2: 20, num1: 24, address: 'Shanghai' }
              ]
            }
          }
        }
        `
      ]
    }
  }
}
</script>
