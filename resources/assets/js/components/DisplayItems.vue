<template>
    <div>
        <h1>Items</h1>
        <div class="row">
            <div class="col-md-12"></div>
            <div class="col-md-2">
                <router-link :to="{ name: 'CreateItem' }" class="btn btn-outline-primary">Create a new Item</router-link>
            </div>
            <table class="table table-hover">
                <thead>
                <tr>
                    <td>ID</td>
                    <td>Item Name</td>
                    <td>Item Prices</td>
                    <td>Actions</td>
                </tr>
                </thead>
                <tbody>
                <tr v-for="item in items">
                    <td>{{ item.id }}</td>
                    <td>{{ item.name }}</td>
                    <td>{{ item.price }}</td>
                    <td>
                        <router-link :to="{ name: 'EditItem', params: { id: item.id } }" class="btn btn-outline-primary">Edit</router-link>
                        <button class="btn btn-outline-danger" v-on:click="deleteItem(item.id)">Delete</button>
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
            return{
                items :[]
            }
        },
        created: function() {
            this.fetchItems();
        },
        methods: {
            fetchItems() {
                let url = 'http://localhost:8000/items';
                this.axios.get(url).then((response) => {
                    this.items = response.data;
                })
            },
            deleteItem(id) {
                let url = `http://localhost:8000/items/${id}`;
                this.axios.delete(url).then((response) => {
                    this.fetchItems();
                });
            }
        }
    }
</script>