<template>
    <div>
        <h1>Create a new Item</h1>
        <router-link :to="{ name: 'DisplayItems' }" class="btn btn-success">Return to Items</router-link>
        <hr>
        <form v-on:submit.prevent="addItem">
            <div class="row">
                <div class="col-sm-6">
                    <div class="form-group">
                        <input type="text" placeholder="Name" class="form-control" v-model="item.name">
                    </div>
                </div>
                <div class="col-sm-6">
                    <div class="form-group">
                        <input type="text" placeholder="Price" class="form-control" v-model="item.price">
                    </div>
                </div>
                <button class="btn btn-outline-primary">Add Item</button>
            </div>
        </form>
    </div>
</template>
<script>
    export default{
        data() {
            return {
                item: {}
            }
        },
        methods: {
            addItem() {
                let url = `http://localhost:8000/items`;

                this.axios.post(url, this.item).then((response) => {
                    this.$router.push({name: 'DisplayItems'})
                }).catch((response) => {
                    console.log(response);
                })
            }
        }
    }
</script>