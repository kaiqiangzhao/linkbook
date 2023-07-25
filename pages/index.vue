<template>
  <div class="flex flex-col mx-auto max-w-2xl sm:items-top sm:pt-0">
    <div class="w-full mx-auto min-h-screen">
      <div class="flex justify-between m-5 items-center">
        <div class="text-2xl  font-semibold flex justify-left items-center text-blue-600">
          <img class="w-7 mr-2" :src="require('static/logo.png')" alt="My Image">
          <p class="">LinkBook</p>
        </div>
        <div class="text-base text-gray-500 font-semibold">
          <nuxt-link to="/about" class="hover:text-gray-800">关于</nuxt-link>
          <a class="ml-5 hover:text-gray-800" href="https://wenjuan.feishu.cn/m?t=sll8sfw6mjOi-enu6">推荐</a>
        </div>
      </div>
      <div class="m-5 divide-y divide-gray-100">
        <LinkCard v-for="(linkcard, index) in linkcards" :linkcard="linkcard" :key="index" class="mx-auto py-5"/>
      </div>
    </div>
    <footer class="w-full flex justify-center p-5">
      <div class="text-gray-400 text-xs text-center">
        <p>Copyright © 2023</p>
        <p>Powered By Spirit Of Exploration</p>
      </div>
    </footer>
  </div>
</template>

<script>
import LinkCard from "@/components/LinkCard.vue";

const linkcardData = require.context('~/data/', false, /linkcard.*\.json$/)

export default {
  name: 'IndexPage',
  components: {
    LinkCard
  },
  data() {
    return {
      linkcards: []
    }
  },
  mounted() {
    const fileNames = linkcardData.keys().reverse();
    const regex = /(\d{4})(\d{2})(\d{2})/;
    const today = new Date();
    for (let i = 0; i < fileNames.length; i++) {
      const match = fileNames[i].match(regex);
      if (match) {
        const year = match[1];
        const month = match[2] - 1;
        const day = match[3];
        const date = new Date(year, month, day);
        if (date > today) {  // 只展示小于等于今天的数据
          continue
        }
        this.linkcards = this.linkcards.concat(linkcardData(fileNames[i]))
      }
    }
  },
}
</script>
