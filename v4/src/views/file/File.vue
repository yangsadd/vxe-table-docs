<template>
  <div>
    <p class="tip">
      文件操作<br>
    </p>

    <h3>{{ $t('读取文件') }}</h3>
    <demo-block>
     <template v-slot:source>
        <p>
          <vxe-button @click="clickEvent1">读取一个文件</vxe-button>
          <vxe-button @click="clickEvent2">读取指定类型文件</vxe-button>
          <vxe-button @click="clickEvent3">读取多个文件</vxe-button>
        </p>
      </template>
      <template v-slot:highlight>
        <pre><pre-code class="xml">{{ demoCodes[0] }}</pre-code></pre></template>
    </demo-block>

    <h3>{{ $t('保存文件') }}</h3>
    <demo-block>
     <template v-slot:source>
        <p>
          <vxe-button @click="clickEvent6">保存为txt文件</vxe-button>
          <vxe-button @click="clickEvent7">保存为html文件</vxe-button>
        </p>
      </template>
      <template v-slot:highlight>
        <pre><pre-code class="xml">{{ demoCodes[1] }}</pre-code></pre></template>
    </demo-block>

    <h3>{{ $t('下载文件') }}</h3>
    <demo-block>
     <template v-slot:source>
        <p>
          <vxe-button @click="clickEvent10">下载文件</vxe-button>
        </p>
      </template>
      <template v-slot:highlight>
        <pre><pre-code class="xml">{{ demoCodes[2] }}</pre-code></pre></template>
    </demo-block>

    <!-- <p class="demo-code">{{ $t('app.body.button.showCode') }}</p>

    <pre>
      <pre-code class="xml">{{ demoCodes[0] }}</pre-code>
      <pre-code class="typescript">{{ demoCodes[1] }}</pre-code>
    </pre> -->
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { VXETable } from 'vxe-table'

export default defineComponent({
  setup () {
    const clickEvent1 = async () => {
      try {
        const { file } = await VXETable.readFile()
        VXETable.modal.alert(`文件名：${file.name}，文件大小：${file.size}`)
      } catch (e) {}
    }

    const clickEvent2 = async () => {
      try {
        const { file } = await VXETable.readFile({
          types: ['xlsx', 'html']
        })
        VXETable.modal.alert(`文件名：${file.name}，文件大小：${file.size}`)
      } catch (e) {}
    }

    const clickEvent3 = async () => {
      try {
        const { files } = await VXETable.readFile({
          multiple: true
        })
        VXETable.modal.alert(`共：${files.length} 个文件`)
      } catch (e) {}
    }

    const clickEvent6 = () => {
      VXETable.saveFile({
        filename: '文本',
        type: 'txt',
        content: '内容xxx'
      })
    }

    const clickEvent7 = () => {
      VXETable.saveFile({
        filename: '页面',
        type: 'html',
        content: '<html><head></head><body>内容xx</body></html>'
      })
    }

    const clickEvent10 = () => {
      // 请求文件
      fetch('https://pic2.zhimg.com/50/v2-f7031359103859e1ed38559715ef5f3f_hd.gif')
        .then(response => response.blob())
        .then(blob => {
          // 下载到本地
          VXETable.saveFile({ filename: '图片', type: 'gif', content: blob })
        })
    }

    return {
      clickEvent1,
      clickEvent2,
      clickEvent3,
      clickEvent6,
      clickEvent7,
      clickEvent10,
      demoCodes: [
        `
        <p>
          <vxe-button @click="clickEvent1">读取一个文件</vxe-button>
          <vxe-button @click="clickEvent2">读取指定类型文件</vxe-button>
          <vxe-button @click="clickEvent3">读取多个文件</vxe-button>
        </p>

        import { defineComponent } from 'vue'
        import { VXETable } from 'vxe-table'

        export default defineComponent({
          setup () {
            const clickEvent1 = async () => {
              try {
                const { file } = await VXETable.readFile()
                VXETable.modal.alert(\`文件名：\${file.name}，文件大小：\${file.size}\`)
              } catch (e) {}
            }

            const clickEvent2 = async () => {
              try {
                const { file } = await VXETable.readFile({
                  types: ['xlsx', 'html']
                })
                VXETable.modal.alert(\`文件名：\${file.name}，文件大小：\${file.size}\`)
              } catch (e) {}
            }

            const clickEvent3 = async () => {
              try {
                const { files } = await VXETable.readFile({
                  multiple: true
                })
                VXETable.modal.alert(\`共：\${files.length} 个文件\`)
              } catch (e) {}
            }

            return {
              clickEvent1,
              clickEvent2,
              clickEvent3
            }
          }
        `,
        `
        <p>
          <vxe-button @click="clickEvent6">保存为txt文件</vxe-button>
          <vxe-button @click="clickEvent7">保存为html文件</vxe-button>
        </p>

        import { defineComponent } from 'vue'
        import { VXETable } from 'vxe-table'

        export default defineComponent({
          setup () {

            const clickEvent6 = () => {
              VXETable.saveFile({
                filename: '文本',
                type: 'txt',
                content: '内容xxx'
              })
            }

            const clickEvent7 = () => {
              VXETable.saveFile({
                filename: '页面',
                type: 'html',
                content: '<html><head></head><body>内容xx</body></html>'
              })
            }

            return {
              clickEvent6,
              clickEvent7
            }
          }
        }
        `,
        `
        <p>
          <vxe-button @click="clickEvent10">下载文件</vxe-button>
        </p>

        import { defineComponent } from 'vue'
        import { VXETable } from 'vxe-table'

        export default defineComponent({
          setup () {

            const clickEvent10 = () => {
              // 请求文件
              fetch('https://pic2.zhimg.com/50/v2-f7031359103859e1ed38559715ef5f3f_hd.gif')
                .then(response => response.blob())
                .then(blob => {
                  // 下载到本地
                  VXETable.saveFile({ filename: '图片', type: 'gif', content: blob })
                })
            }

            return {
              clickEvent10
            }
          }
        }
        `,
        `
        import { defineComponent } from 'vue'
        import { VXETable } from 'vxe-table'

        export default defineComponent({
          setup () {
            const clickEvent1 = async () => {
              try {
                const { file } = await VXETable.readFile()
                VXETable.modal.alert(\`文件名：\${file.name}，文件大小：\${file.size}\`)
              } catch (e) {}
            }

            const clickEvent2 = async () => {
              try {
                const { file } = await VXETable.readFile({
                  types: ['xlsx', 'html']
                })
                VXETable.modal.alert(\`文件名：\${file.name}，文件大小：\${file.size}\`)
              } catch (e) {}
            }

            const clickEvent3 = async () => {
              try {
                const { files } = await VXETable.readFile({
                  multiple: true
                })
                VXETable.modal.alert(\`共：\${files.length} 个文件\`)
              } catch (e) {}
            }

            const clickEvent6 = () => {
              VXETable.saveFile({
                filename: '文本',
                type: 'txt',
                content: '内容xxx'
              })
            }

            const clickEvent7 = () => {
              VXETable.saveFile({
                filename: '页面',
                type: 'html',
                content: '<html><head></head><body>内容xx</body></html>'
              })
            }

            const clickEvent10 = () => {
              // 请求文件
              fetch('https://pic2.zhimg.com/50/v2-f7031359103859e1ed38559715ef5f3f_hd.gif')
                .then(response => response.blob())
                .then(blob => {
                  // 下载到本地
                  VXETable.saveFile({ filename: '图片', type: 'gif', content: blob })
                })
            }

            return {
              clickEvent1,
              clickEvent2,
              clickEvent3,
              clickEvent6,
              clickEvent7,
              clickEvent10
            }
          }
        }
        `
      ]
    }
  }
})
</script>
