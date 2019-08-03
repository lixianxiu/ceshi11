

<script>
export default {
  name: "menu-nav",
  props: {},
  data() {
    return {
      menu: [
        {
          title: "handle_center",
          id: 1,
          path: ""
        },
        {
          title: "table_job",
          id: 2,
          path: "",
          children: [
            {
              title: " job1",
              id: 2 - 1,
              path: ""
            },
            {
              title: " job2",
              id: 2 - 2,
              path: ""
            },
            {
              title: " job3",
              id: 2 - 3,
              path: ""
            }
          ]
        },
        {
          title: " infomation",
          id: 3,
          path: ""
        }
      ],
      activeIndex: "1",
      activeIndex2: "1"
    };
  },
  render(h) {
    return <div class="my_menu">{this.menuRnder(h, this.menu)}</div>;
  },
  methods: {
    handleSelect(key, keyPath) {
      console.log(key, keyPath);
    },
    menuRnder(h, menu) {
      return (
        <el-menu
          default-active={this.activeIndex2}
          class="el-menu-demo"
          mode="horizontal"
          onSelect={this.handleSelect}
          style={{ backgroundColor: "#545c64" }}
          text-color="#ccc"
          active-text-color="58bc58"
        >
          {menu.map(menu => {
            if (menu.children) {
              return (
                <el-submenu index={menu.id}>
                  {h("template", { slot: "title" }, menu.name)}
                  {menu.children.map(menu => {
                    return (
                      <el-menu-item index={menu.id}>{menu.name}</el-menu-item>
                    );
                  })}
                </el-submenu>
              );
            } else {
              return <el-menu-item index={menu.id}>{menu.title}</el-menu-item>;
            }
          })}
        </el-menu>
      );
    }
  }
};
</script>

