# page
基于vue的轻量级分页插件
npm i
npm run server
引入组件page.vue
import page from '@/components/common/page';
components: {
  page
}

使用组件
<page :pages="pages" :current="current" @change="e => current = e"></page>
