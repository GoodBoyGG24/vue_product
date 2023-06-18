<template>
  <product-form @add-product="addProduct" />
  <product-table :products="products" 
  @delete:product="deleteProduct" 
  @edit:product = "editProduct"
  />
</template>

<script>
import ProductForm from './components/ProductForm.vue'
import ProductTable from './components/ProductTable.vue'
export default {
  name: 'App',
  components: {
    ProductForm,
    ProductTable
  },
  data() {
    return {
      products: [
        {
          id: '1',
          name: 'Acer Swift-3',
          price: '12000000',
          amount: '10'
        },
      ]
    }
  },
  methods: {
    addProduct(product) {
      const lastID =
        this.products.length > 0 ? this.products[this.products.length - 1].id : 0;
      const id = lastID + 1;
      const newProduct = { ...product, id };
      this.products = [...this.products, newProduct]
    },
    deleteProduct(id) {
      this.products = this.products.filter(product => product.id !== id)
    },
    editProduct(id , updatedProduct){
      this.products = this.products.map(product => product.id === id ? updatedProduct : product)
    }
  }
}
</script>

<style scoped></style>
