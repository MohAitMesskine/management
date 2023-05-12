<template>
  <div class="sidebar">
    <el-menu
        active-text-color="#20A0FF"
        text-color="#E5EDF2"
        background-color="#324157"
        default-active="/dashboard"
        class="sidebar-el-menu"
        :collapse="collapse"
        unique-opened
        router
    >
      <template v-for="item in menuItems" :key="item.index">
        <template v-if="item.subs">
          <el-sub-menu :index="item.index" :key="item.index">
            <template #title>
              <i :class="item.icon"></i>
              <span>{{item.title}}</span>
            </template>
            <template v-for="subItem in item.subs">
              <el-sub-menu v-if="subItem.subs" :key="subItem.index" :index="subItem.index">
                <template #title>{{subItem.title}}</template>
                <el-menu-item v-for="(threeItem, i) in subItem.subs" :index="threeItem.index" :key="i">
                  {{threeItem.title}}
                </el-menu-item>
              </el-sub-menu>
              <el-menu-item v-else :index="subItem.index" :key="subItem.index">{{subItem.title}}</el-menu-item>
            </template>
          </el-sub-menu>
        </template>
        <template v-else>
          <el-menu-item :index="item.index" :key="item.index">
            <i :class="item.icon"></i>
            <span>{{item.title}}</span>
          </el-menu-item>
        </template>
      </template>
    </el-menu>
  </div>
</template>

<script>
export default {
  name: "Sidebar",
  data() {
    return {
      menuItems: [
        {
          icon: "el-icon-house",
          index: "/dashboard",
          title: "acceuil",
        },
        {
          icon: "el-icon-tickets",
          index: "/table",
          title: "table",
        },
        {
          icon: "el-icon-document-copy",
          index: "/tabs",
          title: "icon-document",
        },
        {
          icon: "el-icon-notebook-2",
          index: "3",
          title: "icon notebook",
          subs: [
            {
              index: "/form",
              title: "form",
            },
            {
              index: "/upload",
              title: "upload",
            },
            {
              index: "4",
              title: "4",
              subs: [
                {
                  index: "/editor",
                  title: "modificateur",
                },
              ],
            },
          ],
        },
        {
          icon: "el-icon-thumb",
          index: "/icon",
          title: "/icon",
        },
        {
          icon: "el-icon-pie-chart",
          index: "/charts",
          title: "charts",
        },
        {
          icon: "el-icon-basketball",
          index: "/i18n",
          title: "icon-basketball",
        },
        {
          icon: "el-icon-warning-outline",
          index: "7",
          title: "warning-outline",
          subs: [
            {
              index: "/permission",
              title: "permission",
            },
            {
              index: "/404",
              title: "404",
            },
          ],
        }
      ]
    }
  },
  computed: {
    collapse: function () {
      return this.$store.state.collapse;
    }
  }
}
</script>

<style scoped>
.sidebar {
  display: block;
  position: absolute;
  left: 0;
  top: 70px;
  bottom: 0;
  overflow-y: scroll;
}
.sidebar::-webkit-scrollbar {
  width: 0;
}
/*
  not选择器，指含有sidebar-el-menu类，不含el-menu--collapse类的标签
  菜单折叠时，标签会自动增加el-menu--collapse标签
*/
.sidebar-el-menu:not(.el-menu--collapse) {
  width: 250px
}
.sidebar > ul {
  height: 100%;
}

</style>
