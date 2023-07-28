<template>
  <div>
    <el-input-number
      v-model="num"
      :min="0"
      :max="10"
      controls-position="right"
      size="large"
      @change="handleChange"
    />
    <el-menu class="layout-menu">
      <HelloWord v-for="item in menuList" :key="`${item.id}`" :item="item" />
    </el-menu>
  </div>
</template>

<script setup lang="ts">
import HelloWord from "./components/HelloWorld.vue";
import { reactive, toRefs, ref } from "vue";
interface menuType {
  id: number;
  title: string;
  children: menuType[] & any;
}
//菜单列表
let menuList = ref<menuType[]>([]);
let obj = reactive<menuType>({
  id: 0,
  title: "",
  children: [],
});
//级联菜单层级
const num = ref(0);
//控制isOver
const handleChange = () => {
  isOver.value = 1;
  menuList.value = [];
  if (num.value === 0) {
    menuList.value = [];
  } else if (num.value === 1) {
    menuList.value.splice(0, 1, obj);
    menuList.value[0].id = 1;
    menuList.value[0].title = "1-1";
    menuList.value[0].children = [];
  } else {
    //多级菜单
    menuList.value.splice(0, 1, obj);
    menuList.value[0].id = 1;
    menuList.value[0].title = "1-1";
    fn1(menuList.value[0]);
  }
};
//是否还要继续执行
let isOver = ref<number>(1);
//执行菜单添加函数
const fn1 = (item: menuType) => {
  isOver.value++;
  const obj1 = {
    id: 0,
    title: "",
    children: [],
  };
  item.children.splice(0, 1, obj1);
  obj1.id = item.id + 1;
  obj1.title = `${item.id + 1}-${item.id + 1}`;
  //判断是否继续执行fn1函数
  if (isOver.value >= num.value) {
  } else {
    fn1(obj1);
  }
};
</script>

<style lang="scss" scoped></style>
