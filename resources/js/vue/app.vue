<template>
    <div class="todolistContainer">
        <div class="heading">
            <h2 id="title">Todo List</h2>
            <add-item-form
                v-on:reloadlist="getlist()"
            />
        </div>
        <list-view
            :items="items"
            v-on:reloadlist="getlist()"
        />
    </div>
</template>
<script>

import AddItemForm from "./addItemForm";
import ListView from "./listView";
import listItem from "./listItem";
export default {
    components: {
        ListView,
        AddItemForm,
        listItem
    },
    data: function () {
        return {
            items: []
        }
    },
    methods: {
        getlist() {
            axios.get('api/items')
            .then( response => {
                this.items = response.data
            })
            .catch( error => {
                console.log(error);
            })
        }
    },
    created() {
        this.getlist()
    }
}
</script>
<style scoped>
.todolistContainer {
    width: 350px;
    margin: auto;
}
.heading {
    background: #e2e6ea;
    padding: 10px;
}

#title {
    text-align: center;
}

</style>
