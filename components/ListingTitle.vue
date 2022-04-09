<template>
  <div>
    <h1 class="font-semibold text-xl">
      {{ name }}
    </h1>

    <NuxtLink :to="`/store/${store.slug}`" class="underline text-gray-400">{{
      store.name
    }}</NuxtLink>
  </div>
</template>

<script>
export default {
  props: {
    name: { type: String, required: true },
    store: { type: Object, required: true },
  },
}
</script>
