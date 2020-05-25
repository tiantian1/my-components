<template>
  <div class="home">
    <!--部门树-->
    <h2>部门树</h2>
    <tree :data="newZone"></tree>
  </div>
</template>

<script>
// @ is an alias to /src
import tree from "../components/tree/Tree";
export default {
  name: "Home",
  components: {
    tree
  },
  data() {
    return {
      zoneList: [
        {
          id: "1",
          pid: "0",
          name: "name",
          fullname: "fullnamer0",
          isreal: "0",//0:点击不允许选中 1：点击允许选中
          isdelete: "0",
          code: "0001",
          level: "1"
        },
        {
          id: "2",
          pid: "0",
          name: "name",
          fullname: "fullnamer1",
          isreal: "1",
          isdelete: "0",
          code: "0002",
          level: "1"
        },
        {
          id: "3",
          pid: "1",
          name: "name",
          fullname: "fullnamer01",
          isreal: "1",
          isdelete: "0",
          code: "00010001",
          level: "2"
        },
        {
          id: "4",
          pid: "3",
          name: "name",
          fullname: "fullnamer0101",
          isreal: "1",
          isdelete: "0",
          code: "000100010001",
          level: "3"
        }
      ],
       newZone: []
    };
  },
  mounted(){
      this.newZone=this.setTreeData(this.zoneList);
      this.$EventBus.$on('chooseItem',res=>{
        console.info("selected:",res);
      })
  },
  methods:{
     setTreeData(source) {
      let cloneData = JSON.parse(JSON.stringify(source)); // 对源数据深度克隆
      return cloneData.filter(father => {
        // 循环所有项，并添加children属性
        let branchArr = cloneData.filter(child => father.id == child.pid); // 返回每一项的子级数组
        branchArr.length > 0
          ? ((father.children = branchArr), (father.open = false))
          : ""; //给父级添加一个children属性，并赋值
        return father.pid == 0; //返回第一层
      });
    }
  },
    //添加以下语句，在组件beforeDestory的时候销毁。防止多次触发
  beforeDestroy() {
    this.$EventBus.$off("chooseItem");
  }
};
</script>
<style lang="scss" scoped>
</style>
