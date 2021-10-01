<template>
    <div class="bg-red-800 py-5">
        <h2 class="text-3xl text-center text-gray-700 mb-4 text-white">Update Product</h2>
        <div class="bg-white-800 bg-white rounded shadow-lg p-8">
            <form class="mb-4" @submit.prevent="updateProduct">
                <div class="flex flex-col mb-4">
                    <label class="mb-2 uppercase font-bold text-lg text-grey-darkest" for="name">Name</label>
                    <input class="border py-2 px-3 text-grey-darkest" type="text" name="name" id="name" v-model="product.name">
                </div>
                <div class="flex flex-col mb-4">
                    <label class="mb-2 uppercase font-bold text-lg text-grey-darkest" for="detail">Details</label>
                    <input class="border py-2 px-3 text-grey-darkest" type="text" name="detail" id="detail" v-model="product.detail">
                </div>
                <button type="submit" class="btn btn-primary">Update</button>
            </form>

        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            product: {}
        }
    },
    created() {
        this.axios
            .get(`http://localhost:8000/api/products/${this.$route.params.id}`)
            .then((res) => {
                this.product = res.data;
            });
    },
    methods: {
        updateProduct() {
            this.axios
                .patch(`http://localhost:8000/api/products/${this.$route.params.id}`, this.product)
                .then((res) => {
                    this.$router.push({ name: 'home' });
                });
        }
    }
}
</script>
