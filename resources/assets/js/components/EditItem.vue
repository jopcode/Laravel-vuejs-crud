<template>
    <div>
        <h1>Update Item</h1>
        <div class="row">
            <div class="col-md-10"></div>
            <div class="col-md-2"><router-link :to="{ name: 'DisplayItems' }" class="btn btn-success">Return to Items</router-link></div>
        </div>

        <form v-on:submit.prevent="updateItem">
            <div class="form-group">
                <input type="text" placeholder="Name" class="form-control" v-model="item.name">
            </div>

            <div class="form-group">
                <input type="text" placeholder="Price" class="form-control" v-model="item.price">
            </div>

            <div class="form-group">
                <button class="btn btn-outline-primary">Update</button>
            </div>
        </form>
    </div>
</template>
<script>
    export default {
        data() {
            return {
                item: {}
            }
        },
        created: function() {
            this.getItem();
        },
        methods: {
            getItem() {
                let url = `http://localhost:8000/items/${this.$route.params.id}/edit`;
                this.axios.get(url).then((response) => {
                    this.item = response.data;
                });
            },
            updateItem() {
                let url = `http://localhost:8000/items/${this.$route.params.id}`;
                this.axios.patch(url, this.item).then((response) => {
                    this.$router.push({name: 'DisplayItems'});
                })
            }
        }
    }
</script>