<template>
  <div class="coontainer justify-center">
    <div class="w-4/5">
      <product-form @add-product="addProduct" />
    </div>

    
  </div>
  
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
          name: 'Asus Tuf-15 Gaming', 
          price: '12899000',
          amount: '5'
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
