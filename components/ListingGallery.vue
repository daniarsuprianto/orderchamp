<!-- Could have used library such as Swiper, but that's for improvement -->
<template>
  <div>
    <div class="p-2 md:w-2/3 mx-auto">
      <div class="relative overflow-hidden pb-full">
        <img
          :src="images[activeIndex].node.small"
          :alt="`Should have very descriptive name ${activeIndex + 1}`"
          class="absolute h-full w-full object-cover"
        />
      </div>
    </div>

    <ul
      v-if="images.length > 1"
      class="flex md:justify-center overflow-auto gap-2 py-2 px-4 border-b border-t border-gray-200"
    >
      <li
        v-for="(image, index) in images"
        :key="image.node.id"
        class="w-20 flex-shrink-0 border border-gray-200 rounded p-1"
        :class="{ 'border-gray-400': activeIndex === index }"
        @click="activeIndex = index"
      >
        <img :src="image.node.modal" class="h-full w-full object-cover" />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: { images: { type: Array, default: () => [] } },
  data() {
    return {
      activeIndex: 0,
    }
  },
}
</script>
