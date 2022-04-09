<template>
  <div
    v-if="!$fetchState.pending"
    class="container max-w-screen-lg mx-auto py-8"
  >
    <div class="lg:flex gap-6">
      <ListingGallery
        v-if="listing.images.edges.length"
        :images="listing.images.edges"
        class="mb-4 lg:w-3/5"
      />

      <div class="px-4 lg:px-0 flex-grow">
        <div class="flex justify-between items-start">
          <ListingTitle :name="listing.translation.title" :store="store" />

          <SaveAsFavorite :favorite="favorite" @click="toggleFavorite" />
        </div>

        <AddToCart :listing="listing" />
      </div>
    </div>

    <section class="px-4 mt-4 lg:px-0 border-t border-gray-200 pt-2">
      <div class="lg:w-3/5">
        <h2 class="text-lg font-semibold mb-2">Information</h2>
        <p class="whitespace-pre-line">{{ listing.translation.description }}</p>
      </div>
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
  async fetch() {
    await this.fetchObjectData()
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
    toggleFavorite() {
      this.favorite = !this.favorite
    },
  },
}
</script>
