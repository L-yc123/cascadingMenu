<template>
  <div>
    <el-sub-menu v-if="item.children === null" :index="`${item.id}`">
      <template #title>
        <span>{{ item.title }}</span>
      </template>
      <el-menu-item
        v-for="(innerItem, innerIndex) in item.children"
        :key="innerIndex"
        >{{ innerItem.title }}</el-menu-item
      >
    </el-sub-menu>
    <el-sub-menu v-if="item.children !== null" :index="`${item.id}`">
      <template #title>{{ item.title }}</template>
      <HelloWord
        v-for="(it, inI) in item.children"
        :key="inI"
        :item="(it as menuType)"
      />
    </el-sub-menu>
  </div>
</template>

<script setup lang="ts">
import HelloWord from "./HelloWorld.vue";
import { reactive, toRefs, ref } from "vue";
interface menuType {
  id: number;
  title: string;
  children: menuType;
}
const props = defineProps<{
  item: menuType;
}>();
const { item } = toRefs(props);
</script>

<style lang="scss" scoped></style>
