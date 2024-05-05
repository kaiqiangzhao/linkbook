<template>
  <div class="flex flex-col mx-auto max-w-2xl sm:items-top sm:pt-0">
    <div class="w-full mx-auto min-h-screen">
      <div class="flex justify-between m-5 items-center">
        <div class="text-2xl font-semibold flex justify-left items-center ">
          <img class="w-7 mr-2" :src="require('static/logo.png')" alt="My Image">
          <p class="">LinkBook</p>
        </div>
        <div class="text-base text-gray-500 font-semibold flex space-x-5 items-center">
          <nuxt-link to="/about" class="hover:text-gray-800">关于</nuxt-link>
          <a class="hover:text-gray-800" href="https://wenjuan.feishu.cn/m?t=s3m8Ey360aOi-6ttv">
            <button class="bg-blue-600 text-gray-200 py-1 px-3">
              推荐
            </button>
          </a>
        </div>
      </div>
      <div class="m-5 divide-y">
        <LinkCard v-for="(linkcard, index) in linkcards" :linkcard="linkcard" :key="index" class="mx-auto py-5"/>
      </div>
    </div>
    <footer class="w-full flex justify-center p-5">
      <div class="text-gray-400 text-xs text-center space-y-2">
        <p class="space-x-2">
          <span>Copyright © 2023</span>
          <a class="hover:text-gray-800" href="https://wenjuan.feishu.cn/m?t=s9vU4S0KXrOi-jq6s">反馈建议</a>
          <a class="hover:text-gray-800" href="https://github.com/kaiqiangzhao/linkbook">Github</a></p>
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
        let linkcards = linkcardData(fileNames[i])
        for (let j = 0; j < linkcards.length; j++) {
          // 获取年、月、日
          const year = date.getFullYear();
          const month = date.getMonth() + 1; // 月份从 0 开始，需要加 1
          const day = date.getDate();

          // 将年月日格式化为字符串
          linkcards[j]["published_date"] = `${year}-${month < 10 ? '0' + month : month}-${day < 10 ? '0' + day : day}`
        }
        this.linkcards = this.linkcards.concat(linkcards)
      }
    }
  },
}
</script>
