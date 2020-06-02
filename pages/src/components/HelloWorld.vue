<template>
  <div>
    <page :pages="pages" :current="current" @change="e => current = e"></page>
  </div>
</template>

<script>
  import page from '@/components/common/page';
  export default {
    components: {
      page
    },
    data() {
      return {
        pages: 15, //总页数
        current: 1 //当前页
      }
    }
  }
</script>

<style>

</style>
