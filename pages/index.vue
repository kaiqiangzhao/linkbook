<template>
  <div class="mx-auto max-w-2xl sm:items-top sm:pt-0">
  <div class="w-full mx-auto">
    <div class="flex justify-between font-bold m-6">
      <div class="text-blue-600 text-2xl">
        <p
          class="bg-gradient-to-r from-blue-300 via-blue-500 to-blue-700 bg-[length:100%_4px] bg-no-repeat bg-bottom">
          下划线
        </p>
      </div>
      <div class="text-1xl text-gray-600">
        <nuxt-link to="/about">关于</nuxt-link>
        <a class="ml-6" href="https://wenjuan.feishu.cn/m?t=s3m8Ey360aOi-6ttv">推荐</a>
      </div>
    </div>
    <div class="m-6">
      <LinkCard v-for="(linkcard, index) in linkcards" :linkcard="linkcard" :key="index" class="mx-auto"/>
    </div>
  </div>
  </div>
</template>

<script>
import LinkCard from "@/components/LinkCard.vue";
const linkcardData = require.context('~/static/data/', false, /linkcard.*\.json$/)

export default {
  name: 'IndexPage',
  components: {
    LinkCard
  },
  data(){
    return {
      linkcards: []
    }
  },
  mounted() {
    const fileNames = linkcardData.keys().reverse();
    for (let i = 0; i < fileNames.length; i++) {
      this.linkcards = this.linkcards.concat(linkcardData(fileNames[i]))
    }
  },
}
</script>

