<template>
    <table class="min-w-full text-center">
        <thead class="bg-gray-200 border-b">
            <tr>
                <th scope="col" class="text-sm font-medium text-gray-900 px-6 py-4 text-center">
                    Product Name
                </th>
                <th scope="col" class="text-sm font-medium text-gray-900 px-6 py-4 text-center">
                    Product Price
                </th>
                <th scope="col" class="text-sm font-medium text-gray-900 px-6 py-4 text-center">
                    Product Amount
                </th>
                <th scope="col" class="text-sm font-medium text-gray-900 px-6 py-4 text-center">
                    Edit Product
                </th>
                <th scope="col" class="text-sm font-medium text-gray-900 px-6 py-4 text-center">
                    Delete Product
                </th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="product in products" :key="product.id" class="text-center border-b">
                <td v-if="editing === product.id">
                    <input type="text" v-model="product.name">
                </td>
                <td v-else>
                    {{ product.name }}
                </td>
                <td v-if="editing === product.id">
                    <input type="number" v-model="product.price">
                </td>
                <td v-else>
                    {{ product.price }}
                </td>
                <td v-if="editing === product.id">
                    <input type="number" v-model="product.amount">
                </td>
                <td v-else>
                    {{ product.amount }}
                </td>
                <td v-if="editing === product.id">
                    <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" 
                    @click="editProduct(product)">Save</button>
                    
                    <button class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded"
                    @click="cancelEdit(product)">Cancel</button>
                </td>
                <td v-else>
                    <button @click="editMode(product)">Edit</button>
                </td>
                <td>
                    <button @click="$emit('delete:product', product.id)">Delete</button>
                </td>
            </tr>
        </tbody>
    </table>
</template>
  
<script>
export default {
    name: 'ProductTable',
    data() {
        return {
            editing: null,
            cachedProduct: null,
        };
    },
    methods: {
        editMode(product) {
            this.cachedProduct = { ...product };
            this.editing = product.id;
        },

        cancelEdit(product) {
            Object.assign(product, this.cachedProduct);
            this.editing = null;
        },

        editProduct(product) {
            if (product.name === '' || product.price === '' || product.amount === '') {
                return;
            }
            this.$emit('edit:product', product.id, product);
            this.editing = null;
        },
    },
    props: {
        products: {
            type: Array,
            required: true,
        },
    },
};
</script>