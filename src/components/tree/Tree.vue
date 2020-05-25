<template>
  <ul class="tree-menu">
    <li v-for="(item, index) in data" :key="index">
      <div class="list-item">
        <span @click="chooseZone(item)">{{ item.fullname || item.name }}</span>
        <i class="icon"  v-if="item.children" @click="toggle(item)" ></i>
      </div>
      <tree-menu v-if="item.open" :data="item.children"></tree-menu>
    </li>
  </ul>
</template>
<script>
export default {
  name: "treeMenu",
  props: {
    data: Array
  },
  data() {
    return {};
  },
  methods: {
    toggle(item) {
      item.open = !item.open;
    },
    chooseZone(item) {
      if (item.isreal == "1") {
        this.$EventBus.$emit("chooseItem", item);
      } else {
        item.open = !item.open;
      }
    }
  }
};
</script>
<style lang="scss" scoped>
.tree-menu {
  padding-left: 0.4rem;
  font-size: 1.4rem;
  list-style: none;

  .list-item {
    height: 2rem;
    line-height: 2rem;
    padding: 0 1rem;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    border-bottom: 1px solid #eeeeee;
    display: flex;
    justify-content: space-between;
    align-items: center;
    span {
      max-width: 24rem;
      overflow: hidden;
      text-overflow: ellipsis;
    }
    .icon{
      background: url('./img/aui-icon-right.png') no-repeat;
      background-size: 1rem 1rem;
      width: 1rem;
      height: 1rem;
    }
  }
}
</style>