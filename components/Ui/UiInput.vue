<template>
  <input
    class="w-full py-2 px-2 border border-gray-200 rounded-sm focus:outline-none h-11 items-center"
    :class="{ 'border-red-500': $attrs.invalid }"
    v-on="inputListeners"
  />
</template>

<script>
export default {
  computed: {
    inputListeners() {
      const vm = this
      return Object.assign({}, this.$listeners, {
        input(event) {
          vm.$emit('input', event.target.value)
        },
      })
    },
  },
}
</script>
