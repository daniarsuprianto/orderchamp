<template>
  <UiButton variant="tertiary" @click="$emit('click')">
    <Component
      :is="favorite ? 'BookmarkSolidIcon' : 'BookmarkIcon'"
      class="w-6 h-6"
    />
  </UiButton>
</template>

<script>
import BookmarkIcon from '@/assets/icons/bookmark.svg'
import BookmarkSolidIcon from '@/assets/icons/bookmark-solid.svg'

export default {
  components: { BookmarkIcon, BookmarkSolidIcon },
  props: { favorite: { type: Boolean } },
}
</script>
