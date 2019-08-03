<template>
  <div class="mapData">
    <el-row :gutter="20">
      <el-col :span="12">
        <letfDataMap :data="tableData" :columns="leftcolumns"></letfDataMap>
      </el-col>
      <el-col :span="12">
        <letfDataMap save="1" :data="tableData" :columns="rightcolumns" @handleData="handleData1"></letfDataMap>
      </el-col>
    </el-row>
    <el-row>
      <el-table :data="selectData">
        <template v-if="selectData.length>0">
          <el-table-column v-for="col in bottomcolumns" :key="col.prop" v-bind="col"></el-table-column>
        </template>
      </el-table>
    </el-row>
  </div>
</template>

<script>
import { debuglog } from "util";
export default {
  name: "tabel-datamap",
  components: {
    letfDataMap: () => import("./tableMap.vue")
  },
  data() {
    return {
      radioValue: 3,
      checkValue: [],
      selectData: [],
      tableData: [
        {
          interfaceId: 1,
          desc: "2016-05-02",
          englishName: "a_b_c_d_ddd",
          chinaName: "上海市普陀区金沙江路 1518 弄",
          sensitive: "no"
        },
        {
          interfaceId: 2,
          desc: "2016-05-04",
          englishName: "a_b_c_d_ddd",
          sensitive: "no",
          chinaName: "上海市普陀区金沙江路 1517 弄"
        },
        {
          interfaceId: 3,
          desc: "2016-05-01",
          englishName: "a_b_c_d_ddd",
          sensitive: "no",
          chinaName: "上海市普陀区金沙江路 1519 弄"
        },
        {
          interfaceId: 4,
          desc: "2016-05-03",
          englishName: "a_b_c_d_ddd",
          sensitive: "no",
          chinaName: "上海市普陀区金沙江路 1516 弄"
        }
      ],
      leftcolumns: [
        {
          label: "字段英文名",
          prop: "englishName",
          formatter: (row, column, celslValue, index) => {
            return (
              <div>
                <i class="el-icon-time"></i>
                <span style="margin-left: 10px">{row.englishName}</span>
              </div>
            );
          }
        },
        {
          label: "字段中文名",
          prop: "chinaName"
        },
        {
          label: "字段描述",
          prop: "desc",
          icon: "el-icon-time"
        },

        {
          label: "选取",
          prop: "select_raido",
          formatter: (row, column, celslValue, index) => {
            // console.log(row);

            return (
              <el-radio
                value={this.radioValue}
                label={index}
                onChange={val => this.radioChange(index, row)}
              >
                &nbsp;
              </el-radio>
            );
          }
        }
      ],
      rightcolumns: [
        {
          label: "表英文名",
          prop: "englishName"
        },
        {
          label: "表中文名",
          prop: "chinaName"
        },
        {
          label: "元数据描述",
          prop: "desc"
        },
        {
          label: "是否敏感",
          prop: "sensitive"
        },
        {
          label: "选取",
          prop: "select_raido",
          formatter: (row, column, celslValue, index) => {
            // console.log(row);

            return (
              <el-checkbox
                value={this.checkValue}
                label={row.interfaceId}
                onChange={val => this.checkChange(val, row.interfaceId, row)}
              >
                &nbsp;
              </el-checkbox>
            );
          }
        }
      ],
      bottomcolumns: [
        {
          label: "Schema",
          prop: "englishName"
        },
        {
          label: "表名",
          prop: "sensitive"
        },
        {
          label: "字段名",
          prop: "chinaName"
        },
        {
          label: "操作",
          prop: "delet_data",
          formatter: (row, column, index) => {
            return (
              <el-button onClick={val => this.deletData(row, column, index)}>
                删除
              </el-button>
            );
          }
        }
      ]
    };
  },
  //   computed: {
  //     selectData() {
  //       return this.selectData;
  //     }
  //   },
  methods: {
    radioChange(e, row) {
      // debugger
      this.radioValue = e;
    },
    checkChange(val, id, row) {
      //if find it ,return INdex or -1;
      const curIndex = this.checkValue.findIndex(item => item === id);
      //   debugger;
      const has = !!val && curIndex === -1;
      //   debugger
      if (has) {
        this.checkValue.push(id);
      } else {
        this.checkValue.splice(curIndex, 1);
      }
    },
    //过滤选取的对应的对象
    handleData1(e) {
      console.log(e);
      // debugger
      //   const arr = [];
      //   this.tableData.filter(item => {
      //     return this.checkValue.forEach(id => {
      //       if (item.interfaceId === id) {
      //         arr.push(item);
      //       }
      //     });
      //   });
      //   优雅的写法研究
      const data2 = this.tableData.reduce((cur, next) => {
        this.checkValue.forEach(id => {
          id === next.interfaceId && cur.push(next);
        });
        return cur;
      }, []);
      console.log(data2);
      //   debugger
      this.selectData = data2;
    },
    deletData(row, column, index) {
      const h = this.$createElement;
      this.$msgbox({
        title: "message",
        message: h("p", null, [h("p", "are you  sure to delete it?")]),
        showCancelButton: true,
        confirmButton: "sure",
        cancelButton: "no",
        beforClose: (action, instance, done) => {
          if (action === "comfirm") {
            setTimeout(() => {
              done();
            }, 300);
          } else {
            done();
          }
        }
      })
        .then(action => {
          this.selectData = this.selectData.filter(
            col => col.interfaceId !== row.interfaceId
          );
          this.$message({
            type: "success ",
            message: "you delete it see you "
          });
        })
        .catch(action => {
          return;
          //   this.$message({
          //     type: "info",
          //     message:
          //       action === "cancel" ? "no delete it" : "停留在当前页面"
          //   });
        });
    }
  }
};
</script>

<style >
</style>
