<template>
    <div class="bg-red-800 py-5">
        <h2 class="text-3xl text-center text-gray-700 mb-4 text-white">Product List</h2>
        <div class='overflow-x-auto w-full'>
            <table class='mx-auto max-w-4xl w-full whitespace-nowrap rounded-lg bg-white divide-y divide-gray-300 overflow-hidden'>
                <thead class="bg-gray-900">
                <tr class="text-white text-left">
                    <th class="font-semibold text-sm uppercase px-6 py-4"> ID </th>
                    <th class="font-semibold text-sm uppercase px-6 py-4"> Name </th>
                    <th class="font-semibold text-sm uppercase px-6 py-4 text-center"> Detail </th>
                    <th class="font-semibold text-sm uppercase px-6 py-4 text-center"> Actions </th>
                </tr>
                </thead>
                <tbody class="divide-y divide-gray-200">
                <tr v-for="product in products" :key="product.id">
                    <td class="px-6 py-4">
                        <div class="flex items-center space-x-3">

                            <div>
                                <p> {{ product.id }}</p>
                            </div>
                        </div>
                    </td>
                    <td class="px-6 py-4">
                        <p class=""> {{ product.name }} </p>
                    </td>
                    <td class="px-6 py-4">
                        <p class=""> {{ product.detail }} </p>
                    </td>
                    <td class="px-6 py-4 text-center">
                        <router-link :to="{name: 'edit', params: { id: product.id }}" class="btn btn-success">Edit</router-link>
                        <button class="btn btn-danger" @click="deleteProduct(product.id)">Delete</button>
                    </td>
                </tr>

                </tbody>
            </table>
        </div>
    </div>

</template>

<script>
export default {
    data() {
        return {
            products: []
        }
    },
    created() {
        this.axios
            .get('http://localhost:8000/api/products/')
            .then(response => {
                this.products = response.data;
            });
    },
    methods: {
        deleteProduct(id) {
            this.axios
                .delete(`http://localhost:8000/api/products/${id}`)
                .then(response => {
                    let i = this.products.map(data => data.id).indexOf(id);
                    this.products.splice(i, 1)
                });
        }
    }
}
</script>
