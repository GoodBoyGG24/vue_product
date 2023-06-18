<template>
    <div class="p-12">
        <form @submit.prevent="handleSubmit">
            <div class="mb-5">
                <label for="name" class="mb-3 block text-base font-medium text-gray-900">
                    Product Name
                </label>
                <input type="text" placeholder="Product name" v-model="product.name" ref="first"
                    :class="{ 'has-error': submitting && invalidName }" @focus="clearStatus" @="clearStatus"
                    class="w-full rounded-md border border-gray-300 bg-white py-3 px-6 text-base font-medium text-gray-900 focus:outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200" />
            </div>
            <div class="mb-5">
                <label for="price" class="mb-3 block text-base font-medium text-gray-900">
                    Product Price
                </label>
                <input type="number" placeholder="Product price" v-model="product.price"
                    :class="{ 'has-error': submitting && invalidPrice }" @focus="clearStatus"
                    class="w-full rounded-md border border-gray-300 bg-white py-3 px-6 text-base font-medium text-gray-900 focus:outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200" />
            </div>
            <div class="mb-5">
                <label for="amount" class="mb-3 block text-base font-medium text-gray-900">
                    Product Amount
                </label>
                <input type="number" placeholder="Product Amount" v-model="product.amount"
                    :class="{ 'has-error': submitting && invalidAmount }" @focus="clearStatus"
                    class="w-full rounded-md border border-gray-300 bg-white py-3 px-6 text-base font-medium text-gray-900 focus:outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200" />
            </div>
            <p v-if="error && submitting" class="error-message">
                Please fill out all required fields
            </p>
            <p v-if="success" class="success-message">
                Inserting product successfully
            </p>
            <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
                Add Product
            </button>
        </form>
    </div>
</template>

<script>
export default {
    name: "ProductForm",
    data() {
        return {
            submitting: false,
            error: false,
            success: false,

            product:{
                name: '',
                price: '',
                amount: ''
            }
        };
    },
    methods: {
        handleSubmit() {
            this.submitting = true;
            this.clearStatus();

            if (this.invalidName || this.invalidPrice || this.invalidAmount) {
                this.error = true;
                return;
            }

            this.$emit("add-product", this.product);
            this.$refs.first.focus();

            this.product = {
                name: "",
                price: "",
                amount: "",
            };
            this.error = false;
            this.success = true;
            this.submitting = false;
        },
        clearStatus() {
            this.success = false;
            this.error = false;
        },
    },
    computed: {
        invalidName() {
            return this.product.name === "";
        },
        invalidPrice() {
            return this.product.price === "";
        },
        invalidAmount() {
            return this.product.amount === "";
        },
    },
};
</script>
  
<style scoped>
.error-message {
    color: red;
}

.success-message {
    color: green;
}
</style>