<template>
  <div>
    <ListingVariants
      v-if="listing.variants.edges.length"
      class="my-4"
      :variants="listing.variants.edges"
      @totalPriceChange="totalPrice = $event"
    />

    <UiButton class="w-full justify-between mb-2"
      ><span>Add to Cart</span>{{ formattedTotalPrice }}</UiButton
    >

    <StoreOrderHighlights :listing="listing" />
  </div>
</template>

<script>
export default {
  props: { listing: { type: Object, required: true } },
  data() {
    return {
      totalPrice: 0,
    }
  },
  computed: {
    formattedTotalPrice() {
      if (this.totalPrice <= 0) {
        return '-'
      }

      return new Intl.NumberFormat('nl-NL', {
        style: 'currency',
        currency: 'EUR',
      }).format(this.totalPrice)
    },
  },
  methods: {
    calculatePrice(price) {
      this.totalPrice += price
    },
  },
}
</script>
