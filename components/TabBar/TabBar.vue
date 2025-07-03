<template>
<Tabbar v-model="active" active-color="#ee0a24">
  <TabbarItem icon="home-o">首页</TabbarItem>
  <TabbarItem icon="logistics">逛</TabbarItem>
  <TabbarItem icon="chat-o">消息</TabbarItem>
  <TabbarItem icon="cart-o">购物车</TabbarItem>
  <TabbarItem icon="contact-o">我的</TabbarItem>
</Tabbar>
</template>

<script setup>
import { ref } from 'vue';
import { Tabbar, TabbarItem } from 'vant';

const active = ref(0); // 初始值为 0，表示默认选中第一个标签

</script>

<style lang="scss" scoped>

</style>