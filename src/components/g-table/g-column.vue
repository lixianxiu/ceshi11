<script>
import {get, set} from 'loadsh'
// import mixinOptionExtensions from './mixin-package-option.js'
let len = 0 // 全局变量  更正列索引

/**
 * 转换为大小驼峰命名
 * abc-efg => abcEfg
 */
export const toCamelCase = str => {
  return str.indexOf('-') !== -1
    ? str.replace(/-([a-zA-Z])/g, ($0, $1) => $1.toUpperCase())
    : str
}

export default {
  name: 'table-column',
  props: {
    columns: {
      type: Array,
      required: true
    },
    data: Array
  },
  data() {
    return {}
  },
  render(h) {
    console.log(this.columns,this.data)
    return h('div', this.renderColumns(h, this.columns))
  },
  methods: {
    renderColumns(h, columns) {
      return (
        columns &&
        columns.map((col, index) => {
          let columnIndex
          len = col.children ? len : len + 1
          columnIndex = len - 1
          return h(
            'el-table-column',
            {
              props: Object.assign({}, this.$attrs, col),
              scopedSlots: {
                default: scope => {
                  const params = {
                    roIndex: scope.$index,
                    row: scope.row,
                    columnIndex,
                    prop: col.prop,
                    column:scope.column
                  }
                 return get(scope.row, col.prop)
                }
              }
            },
            this.renderColumns(h, col.children)
          )
        })
      )
    }
  }
}
</script>
