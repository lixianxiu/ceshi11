<template>
  <div id="app">
    <!-- <menu-nav></menu-nav> -->
    <!-- <mapDataFromComponey></mapDataFromComponey>  -->
    <table-add
      stripe
      maxHeitght="400"
      :data="listGood"
      edit
      @addObject="addlist"
      @deletOneObject="deleteOneObject"
    ></table-add>
    <!-- <conditionVue></conditionVue> -->
    <!-- <practice></practice> -->
    <!-- <simple :columns="columns" :data="tableData"></simple> -->
    <!-- <datamap></datamap> -->
    <!-- <gggggg :columns="columns" :data="tableData"></gggggg> -->
    <!-- <g-table :columns="columns" :data="tableData"></g-table> -->
    <!-- <slotcontrol :seen="true  "> -->
    <!-- extend content by slot and the method call slot -->
    <!-- <template v-slot:seeMe>
        <div>I am a extensional content</div>
    </template>-->
    <!-- </slotcontrol> -->
    <!-- <mapData :data="tableData"></mapData> -->
    <!-- <mapData :columns="columns" :data="tableData" type="checked"></mapData> -->
    <!-- <treeInpute></treeInpute> -->
    <!-- <div>
      <treeInpute1></treeInpute1>
    </div>
    <navTab></navTab>
    <div>
      <el-button type="text" @click="popup">点击打开 Message Box</el-button>
    </div>-->
    <!-- <div id="tree"></div> -->
    <!-- <form-text></form-text> -->
    <!-- <render-slot-parent></render-slot-parent> -->
    <!-- <render-form></render-form> -->
    <!-- <jsx-form></jsx-form> -->
    <!-- <edit-table></edit-table> -->
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import Mock from "./components/mock";
// import mapDataFromComponey from "./must/tableMap/tableMap.vue";
export default {
  name: "app",
  components: {
    HelloWorld,
    Mock,
    "menu-nav": () => import("./demo/menu.vue"),
    "table-add": () => import("./must/table-eidt/index.vue"),
    mapDataFromComponey: () => import("./must/tableMap/index.vue"),
    conditionVue: () => import("./must/conditionvue/index.vue"),
    practice: () => import("./components/practiceRender.vue"),
    rendervue: () => import("./components/render.vue"),
    simple: () => import("./components/practiceSimple.vue"),
    datamap: () => import("./components/company/dataMap.vue"),
    gggggg: () => import("./components/company/table/index.vue"),
    "g-table": () => import("./components/g-table/index.vue"),
    slotcontrol: () => import("./goodCom/slotcontrol/index.vue"),
    mapData: () => import("./goodCom/mapData/common.vue"),
    treeInpute: () => import("./goodCom/treeInpute/index.vue"),
    treeInpute1: () => import("./components/treeChek/index.vue"),
    navTab: () => import("./components/navtab/index.vue"),
    formText: () => import("./components/requireTextForm/requireTextForm.vue"),
    // templateSlot: () => import("./demo/template-slot/index.vue"),
    // renderSlotChild: () => import("./demo/render-slot/render-slot-child.vue"),
    renderSlotParent: () => import("./demo/render-slot/render-slot-parent.vue"),
    renderForm: () => import("./demo/render-form/render-form.vue"),
    jsxForm: () => import("./demo/render-form/jsx-form.vue"),
    editTable: () => import("./demo/editTable/index.vue")
  },
  methods: {
    /**
     * 组件加对象
     */
    addlist() {
      // debugger;
      !!this.listGood &&
        this.listGood.push({
          date: "",
          name: "",
          address: "",
          address2: "",
          address3: "",
          address4: ""
        });
    },
    deleteOneObject(index) {
      !!this.listGood && this.listGood.splice(index, 1);
    },
    renderTreeData(data) {
      console.log(data);
      let ul = document.createElement("ul");
      data.forEach(item => {
        let li = document.createElement("li");
        li.innerHTML = item.label;
        ul.append(li);
        if (item.children.length > 0) {
          let childUl = document.createElement("ul");
          item.children.forEach(item => {
            let strs = document.createElement("li");
            strs.innerHTML(item.label);
            childUl.appendChild(strs);
            if (item.children.children > 0) {
              let childUl = document.createElement("ul");
              item.children.forEach(item => {
                let strs = document.createElement("li");
                strs.innerHTML(item.label);
                childUl.appendChild(strs);
              });
            }
          });
        }
      });
      return ul;
    },
    popup() {
      const h = this.$createElement;
      this.$msgbox({
        title: "消息",
        message: h(
          "pre",
          { style: { "white-space": "pre-wrap", "word-wrap": "break-word" } },
          this.list
        ), //[]
        dangerouslyUseHTMLString: true,
        showCancelButton: true,
        confirmButtonText: "确定",
        cancelButtonText: "取消"
        // center: true
      });
    },
    //每行需要截取60个 , 截取成几个组
    sliceStrData(h, data, lenth = 60, arr = []) {
      let sliceLenth = Math.ceil(data.length / lenth);
      for (let i = 0; i < sliceLenth; i++) {
        if (i === 0) {
          arr.push(data.slice(0, lenth));
        } else {
          let timeSlice = (i + 1) * lenth;
          arr.push(data.slice(i * lenth, timeSlice));
        }
      }
      let filterNull = arr.filter(item => item !== "");
      return filterNull;
    },
    listpRender(h, data) {
      let str = data.map(item => {
        return h("p", {}, item);
      });
      return str;
    },
    popupp() {
      this.$alert(
        `<pre style="white-space: pre-wrap;word-wrap: break-word;">${this.list}</pre>`,
        "消息",
        {
          dangerouslyUseHTMLString: true
        }
      );
    }
  },
  mounted() {
    // let ulStr = this.renderTreeData(this.treeData);
    // document.querySelector("#tree").innerHTML = ulStr;
  },
  data() {
    return {
      listGood: [
        {
          date: "12",
          name: "",
          address: "32",
          address2: "",
          address3: "",
          address4: ""
          // edit: false
        },
        
      ],
      list: "",
      columns: [
        {
          type: "index",
          width: "50"
        },
        {
          prop: "name",
          label: "姓名",
          width: "180"
        },
        {
          prop: "address",
          label: "地址",
          width: "180"
        },
        {
          prop: "date",
          label: "日期",
          width: "180"
        }
      ],
      tableData: [
        {
          id: "1",
          date: "2016-05-02",
          name: "asuia",
          address: "上海市普陀区金沙江路 1518 弄"
        },
        {
          id: "2",
          date: "2016-05-04",
          name: "chenLong",
          address: "上海市普陀区金沙江路 1517 弄"
        },
        {
          id: "3",
          date: "2016-05-01",
          name: "qixiao",
          address: "上海市普陀区金沙江路 1519 弄"
        }
      ],
      treeData: [
        {
          label: "一级 1",
          children: [
            {
              label: "二级 1-1",
              children: [
                {
                  label: "三级 1-1-1"
                }
              ]
            }
          ]
        },
        {
          label: "一级 2",
          children: [
            {
              label: "二级 2-1",
              children: [
                {
                  label: "三级 2-1-1"
                }
              ]
            },
            {
              label: "二级 2-2",
              children: [
                {
                  label: "三级 2-2-1"
                }
              ]
            }
          ]
        },
        {
          label: "一级 3",
          children: [
            {
              label: "二级 3-1",
              children: [
                {
                  label: "三级 3-1-1"
                }
              ]
            },
            {
              label: "二级 3-2",
              children: [
                {
                  label: "三级 3-2-1"
                }
              ]
            }
          ]
        }
      ]
    };
  }
};
</script>

<style>
.myMessageBox {
  /* display: block; */
  width: 300px;
  /* white-space: nowrap; */
  /* overflow: hidden; */
}
</style>
