<template>
  <div>
      <article v-for="(content, i) in data.contents">
        <img :src="content.image.url">
        <h2>{{content.title}}</h2>
        <ul>
          <li v-for="(category,i2) in content.categories">
            {{category.tag}}
          </li>
        </ul>
        <button type="button" class="outline" @click="link(`/blogs/${content.id}`)">この記事を読む</button>
      </article>
  </div>
</template>

<script lang="ts">
import {useFetch, defineNuxtComponent} from "#app";
import {useRouter} from "vue-router";

export default defineNuxtComponent({
  async setup(){
    const ctx = useRuntimeConfig()
    const router = useRouter()

    const { data } = await useFetch("/blogs", {
      baseURL: ctx.baseURL,
      headers: {
        "X-MICROCMS-API-KEY": ctx.apiKey,
      },
    });

    const link = (path: string) => {
      router.push(path)
    }
    return {data, link}
  }
})

</script>
