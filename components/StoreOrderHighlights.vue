<template>
  <ul class="border border-gray-200 rounded">
    <li
      v-for="(item, index) in highlightItems"
      :key="index"
      class="flex gap-2 px-4 py-2"
      :class="{ 'border-t border-gray-200': index > 0 }"
    >
      <Component :is="item.icon" class="w-6 h-6" />{{ item.label }}
    </li>
  </ul>
</template>

<script>
import CreditCardIcon from '@/assets/icons/credit-card.svg'
import TruckIcon from '@/assets/icons/truck.svg'

export default {
  components: { CreditCardIcon, TruckIcon },
  props: { listing: { type: Object, required: true } },
  computed: {
    highlightItems() {
      return [
        {
          icon: CreditCardIcon,
          label: '€ 100 order minimum',
        },
        {
          icon: TruckIcon,
          label: `${this.listing.leadTime} shipped directly from brand`,
        },
      ]
    },
  },
}
</script>
