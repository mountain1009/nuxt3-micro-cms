<template>
  <article>
    <div v-html="data.content"></div>
  </article>
</template>

<script lang="ts">
import {useFetch, defineNuxtComponent} from "#app";
import {useRoute} from "vue-router";

export default defineNuxtComponent({
  async setup(){
    const ctx = useRuntimeConfig();
    const route = useRoute()
    const blogId = route.params.id

    if(!blogId) return console.log("idが存在しません")

    const { data } = await useFetch(`/blogs/${blogId}`, {
      baseURL: ctx.baseURL,
      headers: {
        "X-MICROCMS-API-KEY": ctx.apiKey,
      },
    });
    return {data}
  }
})

</script>
