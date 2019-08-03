<template>
  <div>
    <el-form>
      <el-form-item label-width="20%" label="活动名称">
        <el-select ref="reference" v-model="value1" placeholder="请选择" size="mini">
          <el-option :value="value1" class="dataTree-option">
            <el-tree :data="data" :props="defaultProps" @node-click="handleNodeClick">
              <div slot-scope="{node,data}">
                <span>
                  <i class="el-icon-delete-solid"></i>
                  {{data.label}}
                </span>
              </div>
            </el-tree>
          </el-option>
        </el-select>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  name: "select-tree-data",
  components: {
    // treeOption: () => import("./recusionTree.vue")
  },

  data() {
    return {
      form: {},
      value1: "",
      value12: "",
      valueTitle: "",
      data: [
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
      ],
      defaultProps: {
        children: "children",
        label: "label"
      }
    };
  },
  created() {
    console.log(this.value1);
    console.log(this.valueTitle);
  },
  mounted() {
    console.log(this.value1);
    console.log(this.valueTitle);
  },
  methods: {
    handleNodeClick(data) {
      if (!data.children) {
        this.value1 = data.label;
        this.blur();
      }
    },
    blur() {
      // console.log(this.$refs.reference)
      // this.$refs.reference.blur();
    }
  }
};
</script>

<style scoped>
.dataTree-option {
  height: 100%;
}
.dataTree-option {
  padding: 0;
}
.el-select-dropdown__item.selected {
  font-weight: normal;
}
.el-select-dropdown__item.hover,
.el-select-dropdown__item:hover {
  background-color: white;
}
</style>
