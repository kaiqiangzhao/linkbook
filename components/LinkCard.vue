<template>
  <div class="w-full text-left bg-gray-100 rounded p-6 m-6">
    <a class="text-1xl font-semibold text-gray-800 hover:text-blue-600 hover:underline hover:underline-offset-4"
       :href="linkcard.content_url">
      {{ linkcard.content_title }}
    </a>
    <p class="text-sm text-gray-600 mt-4">
      {{ linkcard.content_description }}
    </p>
    <div class="flex justify-between items-center  mt-4">
      <div class="text-xs text-gray-400">{{ linkcard.published_date }} · {{ linkcard.user_url }}</div>
      <div class="text-xs text-blue-600">
        <span class="text-gray-400">推荐者:</span>
        <a
          class="font-semibold bg-gradient-to-r from-blue-300 via-blue-500 to-blue-700 bg-[length:100%_2px] bg-no-repeat bg-bottom"
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
    }
  },
}
</script>

<style scoped>

</style>
