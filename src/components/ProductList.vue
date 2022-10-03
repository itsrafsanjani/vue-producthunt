<script>
import Product from './Product.vue'

export default {
  components: {
    Product,
  },

  data() {
    return {
      products: Seed.products,
    }
  },

  created() {
    this.sortByVotes(this.products)
  },

  methods: {
    handleProductUpVote(productId) {
      const updatedProducts = this.products.map((product) => {
        if (product.id === productId) {
          // update current product.votes
          return { ...product, votes: product.votes + 1 }
        }

        return product
      })

      this.sortByVotes(updatedProducts)
    },

    sortByVotes(products) {
      this.products = products.sort((a, b) => b.votes - a.votes)
    },
  },
}
</script>

<template>
  <div className="ui unstackable items">
    <Product
      v-for="product in products"
      :key="`product-${product.id}`"
      :product="product"
      @onVote="handleProductUpVote"
    />
  </div>
</template>

<style scoped></style>
