<template>
  <div>
    <el-tree
      :data="data"
      show-checkbox
      default-expand-all
      node-key="id"
      ref="tree"
      highlight-current
      :props="defaultProps"
      @node-click="handleNodeClick"
    >
      <div slot-scope="{ node, data }">
        <span>{{data.label}}</span>
        <span>{{data.id}}</span>
      </div>
    </el-tree>

    <div class="buttons">
      <el-button @click="getCheckedNodes">通过 node 获取</el-button>
      <el-button @click="getCheckedKeys">通过 key 获取</el-button>
      <el-button @click="setCheckedNodes">通过 node 设置</el-button>
      <el-button @click="setCheckedKeys">通过 key 设置</el-button>
      <el-button @click="resetChecked">清空</el-button>
      <el-button @click="loadRenderTheTree">重新加载页面假装数据拿到,请重新渲染这个树</el-button>
    </div>
  </div>
</template>



<script>
export default {
  methods: {
    loadRenderTheTree() {
      //  模拟后端给你的id  4  9   需求是把4给过滤掉;然后通过setCheckedKeys 进行渲染
      //实现的方式是递归
      // 1>首先要拿到你的树数据进行递归,累加器实现
      //   let nodeMap = this.nodeMap(this.data);
      let nodeMap = this.lowMap(this.data);
      console.log(nodeMap);
      // neeObject
      // const filterObject = Object.keys(nodeMap).reduce((cur, key) => {
      //   !!!nodeMap[key].children && (cur[key] = nodeMap[key]);
      //   return cur;
      // }, {});
      // needArr
      const filterArr = Object.keys(nodeMap).reduce((cur, key) => {
        !!!nodeMap[key].children && cur.push(key);
        return cur;
      }, []);
      console.log(filterArr);
      const res = ["SSESS-SSSXDXSXSWWW", "SSESS-SSS"];
      // console.log(filterArr.includes("9"));
      const real = res.filter(item => filterArr.includes(item));
      console.log(real);
      this.$refs.tree.setCheckedKeys(real);
    },
    // low 映射
    lowMap(data, temp = {}) {
      data.forEach(item => {
        temp[item.authroistor] = item;
        const hasChild = !!item.children && item.children.length !== 0;
        hasChild && this.lowMap(item.children, temp);
      });
      return temp;
    },
    //史诗级史诗级映射id

    nodeMap(data, temp = {}) {
      return data.reduce((cur, next) => {
        cur[next.id] = next;
        const hasChild = !!next.children && next.children.length !== 0;
        hasChild && this.nodeMap(next.children, cur);
        return cur;
      }, temp);
    },
    getCheckedNodes() {
      console.log(this.$refs.tree.getCheckedNodes());
      console.log(this.checkList);
    },
    getCheckedKeys() {
      console.log(this.$refs.tree.getCheckedKeys());
      console.log(this.$refs.tree);
    },
    setCheckedNodes() {
      this.$refs.tree.setCheckedNodes([
        {
          id: 1,
          label: "一级 1",
          children: [
            {
              id: 4,
              label: "二级 1-1",
              children: [
                {
                  id: 9,
                  label: "三级 1-1-1",
                  children: [
                    {
                      id: 11,
                      label: "三级 2-1-1",
                      children: [
                        { id: 182, label: "4级 1-1-1" },
                        { id: 183, label: "4级 1-1-1" },
                        { id: 184, label: "4级 1-1-1" },
                        { id: 185, label: "4级 1-1-1" },
                        { id: 186, label: "4级 1-1-1" }
                      ]
                    },
                    {
                      id: 12,
                      label: "三级 1-1-2"
                    }
                  ]
                },
                {
                  id: 10,
                  label: "三级 1-1-2"
                }
              ]
            }
          ]
        }
      ]);
    },
    handleNodeClick(data) {
      console.log(data, "asd");
    },
    setCheckedKeys() {
      this.$refs.tree.setCheckedKeys([3]);
    },
    resetChecked() {
      this.$refs.tree.setCheckedKeys([]);
    }
  },

  data() {
    return {
      checkList: [],
      data: [
        {
          authroistor: "SSESS-SSS",
          id: 1,
          label: "SDAS-DSADAS",
          children: [
            {
              authroistor: "SSESS-SSSSC",
              id: 4,
              label: "二级 1-1",
              children: [
                {
                  authroistor: "SSESS-SSSXX",
                  id: 9,
                  label: "三级 1-1-1",
                  children: [
                    {
                      id: 182,
                      label: "4级 1-1-1",
                      authroistor: "SSESS-SSSXXSWX"
                    },
                    {
                      id: 186,
                      label: "4级 1-1-1",
                      authroistor: "SSESS-SSSXDXSX",

                      children: [
                        {
                          id: 191,
                          label: "4级 1-1-1",
                          authroistor: "SSESS-SSSXDXSXSWWW"
                        }
                      ]
                    }
                  ]
                },
                {
                  id: 10,
                  label: "三级 1-1-2",
                  authroistor: "SSESS-SSSXDXSXMM"
                }
              ]
            }
          ]
        },
        {
          id: 2,
          label: "一级 2",
          authroistor: "SSESS-SSSXDXSX22",

          children: [
            {
              id: 5,
              label: "二级 2-1",
              authroistor: "SSESS-SSSX33DXSX"
            },
            {
              id: 6,
              label: "二级 2-2",
              authroistor: "SSES44S-SSSXDXSX"
            }
          ]
        },
        {
          id: 3,
          label: "一级 3",
          authroistor: "SSESSS2S-SSSXDXSX",

          children: [
            {
              id: 7,
              label: "二级 3-1",
              authroistor: "SSESS-SS76-SXDXSX"
            },
            {
              id: 8,
              label: "二级 3-2",
              authroistor: "SSESS-SSS78-9XDXSX"
            }
          ]
        }
      ],
      defaultProps: {
        children: "children",
        label: "label"
      }
    };
  }
};
</script>