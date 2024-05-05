<template>
  <div class="w-full text-left">
    <div class="text-sm text-gray-400 mb-1">
      <span v-if="content_published_year">{{content_published_year + '年 · '}}</span>
      <span v-if="content_url_hostname">{{content_url_hostname}}</span>
    </div>
    <div class="flex">
      <div class="mr-5">
        <a class="text-xl font-semibold hover:underline hover:underline-offset-4"
           :href="linkcard.content.url">
          {{ linkcard.content.title }}
        </a>
        <p class="text-base text-gray-500 mt-5 line-clamp-3">
          {{ linkcard.content.description }}
        </p>
      </div>
    </div>
    <div class="flex justify-between items-center mt-5 text-gray-400 text-sm">
      <div>
        <span>推荐者: </span>
        <a
          class="hover:underline hover:underline-offset-2 hover:text-black"
          :href="linkcard.user.url">
          {{ linkcard.user.nickname }}
        </a>
      </div>
      <div>
        <span v-if="linkcard.published_date">{{linkcard.published_date}}</span>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'LinkCard',
  props: {
    linkcard: {
      content:{
        title: "",
        url: "",
        description: "",
        published_date: "",
      },
      user: {
        nickname: "",
        url: "",
      },
      published_date: "",
    },
  },
  data() {
    return {
      content_url_hostname: "",
      content_published_year: "",
    }
  },
  mounted: function () {
    let hostname = new URL(this.linkcard.content.url).hostname
    this.content_url_hostname = hostname.startsWith("www.") ? hostname.slice(4) : hostname
    let year = new Date(this.linkcard.content.published_date).getFullYear()
    if(year){
      this.content_published_year = year.toString()
    }
  }
}
</script>

<style scoped>

</style>
