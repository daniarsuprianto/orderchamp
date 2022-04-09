<template>
  <div v-if="!$fetchState.pending" class="container pb-12">
    <div class="md:flex">
      <ListingGallery
        v-if="listing.images.edges.length"
        :images="listing.images.edges"
        class="mb-4"
      />

      <div class="px-4">
        <div class="flex justify-between items-start">
          <div>
            <h1 class="font-semibold text-xl">
              {{ listing.translation.title }}
            </h1>
            <NuxtLink
              :to="`/store/${store.slug}`"
              class="underline text-xs text-gray-400"
              >{{ store.name }}</NuxtLink
            >
          </div>
        </div>
    </div>

    <section class="px-4 mt-6">
      <h2 class="font-semibold mb-2">Information</h2>
      <p class="whitespace-pre-line">{{ listing.translation.description }}</p>
    </section>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      store: {},
      listing: {},
      favorite: false,
    }
  },
  fetch() {
    this.fetchObjectData()
  },
  methods: {
    async fetchObjectData() {
      try {
        const response = await fetch(
          'https://gist.githubusercontent.com/Vugario/ca7cc468c344494ccae22b2c835e0c9f/raw/fe4669ee0989e78be1ed9ccd78ba178c695c305a/data.json'
        )
        const jsonData = await response.json()

        this.store = {
          name: jsonData.data.storefrontBySlug.name,
          slug: jsonData.data.storefrontBySlug.slug,
        }

        this.listing = jsonData.data.storefrontBySlug.listing
      } catch (error) {
        console.error(error)
      }
    },
  },
}
</script>
