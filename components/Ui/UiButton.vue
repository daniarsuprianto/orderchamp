<template>
  <Component
    :is="element"
    class="inline-flex px-4 py-2 justify-center rounded h-11 items-center"
    :class="{
      'bg-green-700 text-white': variant === 'primary',
      'bg-gray-800 text-white': variant === 'secondary',
      'border-gray-800': variant === 'secondary-alt',
    }"
    v-on="$listeners"
    ><slot
  /></Component>
</template>

<script>
export default {
  props: {
    variant: {
      type: String,
      default: 'primary',
      validator(value) {
        return ['primary', 'secondary', 'secondary-alt', 'tertiary'].includes(
          value
        )
      },
    },
  },
  computed: {
    element() {
      return this.$attrs.href ? 'a' : 'button'
    },
  },
}
</script>
