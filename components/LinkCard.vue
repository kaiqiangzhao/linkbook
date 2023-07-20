<template>
  <div class="w-full text-left">
    <a class="text-xl font-semibold hover:underline hover:underline-offset-4 hover:text-blue-600"
       :href="linkcard.content_url">
      {{ linkcard.content_title }}
    </a>
    <p class="text-base text-gray-500 mt-5">
      {{ linkcard.content_description }}
    </p>
    <div class="flex justify-between items-center mt-5">
      <div class="text-sm text-gray-500">
        <span class="mr-2" v-if="published_year">{{published_year + '年'}}</span>
        <span v-if="content_url_hostname">{{content_url_hostname}}</span>
      </div>
      <div class="text-sm">
        <span class="text-gray-500">推荐者:</span>
        <a
          class="text-gray-500 underline underline-offset-2 hover:text-gray-800 hover:text-blue-600"
          :href="linkcard.user_url">
          {{ linkcard.user_nickname }}
        </a>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'LinkCard',
  props: {
    linkcard: {
      content_title: "",
      content_url: "",
      content_description: "",
      published_date: "",
      user_nickname: "",
      user_url: "",
    },
  },
  data(){
    return {
      content_url_hostname: "",
      published_year: "",
    }
  },
  mounted: function () {
    let hostname = new URL(this.linkcard.content_url).hostname
    this.content_url_hostname = hostname.startsWith("www.") ? hostname.slice(4) : hostname
    let year = new Date(this.linkcard.published_date).getFullYear()
    if(year){
      this.published_year = year.toString()
    }
  }
}
</script>

<style scoped>

</style>
