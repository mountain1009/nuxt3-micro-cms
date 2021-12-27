<template>
  <section>
    <p>
      {{data}}
    </p>
  </section>
</template>

<script lang="ts">
import {useFetch, defineNuxtComponent} from "#app";

export default defineNuxtComponent({
  async setup(){
    const ctx = useRuntimeConfig();

    const { data } = await useFetch("/categories", {
      baseURL: ctx.baseURL,
      headers: {
        "X-MICROCMS-API-KEY": ctx.apiKey,
      },
    });
    return {data}
  }
})

</script>
