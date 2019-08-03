<script>
 export default {
     name:'rendervue',
    props: {
        list: {
          type: Array,
          default: []
          }, // 数据列表
        columns: {
          type: Array,
          default: []
          }, // 需要展示的列 === prop：列数据对应的属性，label：列名，align：对齐方式，width：列宽
        options: {
          type: Object,
          default: {
            height:300,//默认高度-为了表头固定
            stripe: false, // 是否为斑马纹 table
            highlightCurrentRow: false, // 是否要高亮当前行
            border:false,//是否有纵向边框
            lazy:false,//是否需要懒加载
          },
        }, // table 表格的控制参数
        tableClass:{
          type: String,
          default: 'hxTable'
        },
    },
    //组件
    components: {
      expandDom: {
        functional: true,
        props: {
        row: Object,
        render: Function,
        index: Number,
        column: {
          type: Object,
          default: null
          }
          },
        render: (h, ctx) => {
          const params = {
          row: ctx.props.row,
          index: ctx.props.index
          }
        if (ctx.props.column) params.column = ctx.props.column
          return ctx.props.render(h, params)
        }
      }
    },
    // 数据
    data () {
      return {
        pageIndex: 1,
        multipleSelection: [], // 多行选中
      }
    },
    mounted () {
    },
    computed: {
    },
    methods: {
         loadGetData(row,treeNode,resolve){//懒加载事件数据
 
        },
        handleSelectionChange (val) {// 多行选中
          this.multipleSelection = val
          this.$emit('handleSelectionChange', val)
        },
        clickRow(row, column, event){//单击行事件
          let data = {
            'row':row,
            'column':column,
            'event':event,
          }
          this.$emit('clickRow',data);
        },
        dblclickRow(row, column, event){//双击行事件
          let data = {
            'row':row,
            'column':column,
            'event':event,
          }
          this.$emit('dblclickRow',data);
        },
        contextmenu(row, column, event){//右键行事件-没去掉页面默认的
          let data = {
            'row':row,
            'column':column,
            'event':event,
          }
          this.$emit('contextmenu',data);
        },
        headClick(column, event){//头部列点击事件
          let data = {
            'column':column,
            'event':event,
          }
          this.$emit('headClick',data);
        },
        headcontextmenu(column, event){//头部列右键点击事件
           let data = {
            'column':column,
            'event':event,
          }
          this.$emit('headcontextmenu',data);
        },
        rowChange(currentRow, oldCurrentRow){//当前行发生改变时的事件
           let data = {
            'currentRow':currentRow,
            'oldCurrentRow':oldCurrentRow,
          }
          this.$emit('rowChange',data);
        },
 
    }
  }
</script>
<style>

</style>
