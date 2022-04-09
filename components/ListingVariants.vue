<template>
  <!-- Using old school table instead of fancy flex or grid. Why? Because it's a table, semantically also table. Keep it simple :) -->
  <div>
    <table>
      <thead class="border-b border-gray-200">
        <th class="py-2 font-semibold">Quantity</th>
        <th class="py-2 font-semibold">Variant</th>
        <th class="py-2 font-semibold">Price</th>
        <th class="py-2 font-semibold">MSRP</th>
        <th class="py-2 font-semibold">Stock</th>
      </thead>
      <tbody>
        <tr
          v-for="variant in variants"
          :key="variant.node.id"
          class="border-b border-gray-200"
        >
          <td class="py-1">
            <VariantQuantity
              :max="variant.node.inventory"
              @change="
                (value) => {
                  variant.node.quantity = value
                  calculateTotalPrice()
                }
              "
            />
          </td>
          <td class="px-2">{{ variant.node.options[0].value }}</td>
          <td class="px-2">€{{ variant.node.price }}</td>
          <td class="px-2">€{{ variant.node.msrp }}</td>
          <td class="text-center">
            <StockIndicator
              :availability="getAvailability(variant.node.inventory)"
            />
          </td>
        </tr>
      </tbody>
    </table>

    <StockIndicatorLegend class="mt-2" />
  </div>
</template>

<script>
import { debounce } from 'debounce'

const DEBOUNCE_DURATION = 500

export default {
  props: { variants: { type: Array, default: () => [] } },
  methods: {
    calculateTotalPrice: debounce(function () {
      const totalPrice = this.variants.reduce((price, currentVariant) => {
        price += (currentVariant.node.quantity || 0) * currentVariant.node.price
        return price
      }, 0)

      this.$emit('totalPriceChange', totalPrice)
    }, DEBOUNCE_DURATION),
    getAvailability(inventory) {
      if (inventory >= 10) {
        return 'available'
      }

      if (inventory === 0) {
        return 'unavailable'
      }

      return 'low'
    },
  },
}
</script>
