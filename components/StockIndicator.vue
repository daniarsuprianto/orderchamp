<template>
  <span
    class="inline-block rounded-full w-2 h-2"
    :class="{
      'bg-green': availability === 'available',
      'bg-yellow-400': availability === 'low',
      'bg-gray-400': availability === 'unavailable',
    }"
  ></span>
</template>

<script>
export default {
  props: {
    availability: {
      type: String,
      required: true,
      validator(value) {
        return ['available', 'low', 'unavailable'].includes(value)
      },
    },
  },
}
</script>
