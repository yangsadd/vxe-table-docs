<template>
  <div>
    <CodeLight path="table/scroll/basic/Demo1">
      <template #tip>
        <div>
          虚拟滚动<span class="orange">（最大可以支撑 10w 列、30w 行）</span><br>
          高性能的虚拟渲染，默认情况下，如果设置了 <table-api-link prop="height"/>、<table-api-link prop="max-height"/> 则会根据触发规则自动启用虚拟渲染，触发规则由 <table-api-link prop="scroll-x"/>.<table-api-link prop="gt"/> | <table-api-link prop="scroll-y"/>.<table-api-link prop="gt"/> 设置。虚拟滚动启用后只会渲染指定范围内的可视区数据，其他的数据将被卷去收起，当滚动到可视区时才被渲染出来<br>
          <span class="red">（注：启用虚拟滚动后：<table-api-link prop="show-overflow"/>，<table-api-link prop="show-header-overflow"/>，<table-api-link prop="show-footer-overflow"/> 参数将根据不同场景各自触发生效，无法取消；如果需要支持，将虚拟滚动关闭即可）</span><br>
          <span class="green">（性能优化：横向虚拟滚动由列宽决定性能，每一列的列宽越大就越流畅；纵向虚拟滚动由行高决定性能，每一行的高度越高就越流畅）</span>
        </div>
      </template>

      <template #describe>
        <pre>
          <pre-code>
            | Arrow Up ↑ | 匀速向上滚动数据 |
            | Arrow Down ↓ | 匀速向下滚动数据 |
            | Arrow Left ← | 匀速向左滚动数据 |
            | Arrow Right → | 匀速向右滚动数据 |
            | Page Up | 向上翻页滚动 |
            | Page Down | 向下翻页滚动 |
            | Spacebar | 翻页滚动 |
            | Home | 滚动到顶部 |
            | End | 滚动到底部 |
          </pre-code>
        </pre>
      </template>
    </CodeLight>

    <CodeLight path="table/scroll/basic/Demo2">
      <div>
        手动调优，对于低性能的浏览器可以通过设置 <table-api-link prop="oSize"/> 偏移量来缓解渲染次数，偏移量越大渲染次数就越少，但是每次渲染的耗时就越久<br>
        通过指定 <table-api-link prop="scroll-x"/>={gt: 20} 或 <table-api-link prop="scroll-y"/>={gt: 40} 适合的参数可以手动调优，如果设置 <table-api-link prop="enabled"/>=false 则关闭虚拟滚动<br>
      </div>
    </CodeLight>
  </div>
</template>
