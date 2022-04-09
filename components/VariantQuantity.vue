<template>
  <div class="flex gap-1">
    <UiButton variant="tertiary" :disabled="quantity <= 0" @click="decrease">
      <MinusIcon class="w-4 h-4" />
    </UiButton>

    <div class="w-10 flex-shrink-0">
      <UiInput
        v-model="quantity"
        class="text-center"
        type="number"
        :invalid="invalid"
        min="0"
        :max="max"
        @focus="onFocus"
        @blur="onBlur"
      />
    </div>

    <UiButton variant="tertiary" :disabled="quantity >= max" @click="increase">
      <PlusIcon class="w-4 h-4" />
    </UiButton>
  </div>
</template>

<script>
import PlusIcon from '@/assets/icons/plus.svg'
import MinusIcon from '@/assets/icons/minus.svg'

export default {
  components: { PlusIcon, MinusIcon },
  props: {
    max: { type: [String, Number], default: 0 },
  },
  data() {
    return {
      quantity: 0,
      invalid: false,
    }
  },
  watch: {
    quantity() {
      if (this.quantity <= this.max) {
        this.$emit('change', this.quantity)
      }
    },
  },
  methods: {
    decrease() {
      if (this.quantity > 0) {
        this.quantity--
      }
    },
    increase() {
      if (this.quantity <= this.max) {
        this.quantity++
      }
    },
    onFocus(event) {
      if (event.target.value === '0') {
        event.target.value = ''
      }
    },
    onBlur(event) {
      if (event.target.value === '') {
        event.target.value = 0
      }

      this.invalid = this.quantity > this.max
    },
  },
}
</script>
