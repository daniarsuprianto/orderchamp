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

    <UiButton
      href="mailto:brand@orderchamp.com"
      variant="tertiary"
      class="w-full text-center text-sm"
    >
      <EnvelopeIcon class="w-4 h-4 mr-2" /> Contact the brand
    </UiButton>
  </div>
</template>

<script>
import EnvelopeIcon from '@/assets/icons/envelope.svg'

export default {
  components: { EnvelopeIcon },
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
