<template>
    <div class="todoListContainer">
            <div class="heading">
                <h2 id="title">To Do List</h2>
            </div>
            <add-item-form  v-on:reloadlist="getList()" 
            />
            <list-view 
                :items="items" 
                v-on:reloadlist="getList()"
            />
    </div>
</template>

<script>
import addItemForm from './addItemForm'
import listView from './listView'

export default {
    components:{
        addItemForm,
        listView
    },
    data: function() {
        return {
            items: []
        }
    }, 
    methods: { 
        getList(){
            axios.get('api/items')
            .then( resoponse => {
                this.items = resoponse.data
            })
            .catch( console.error() )
        }
    }, 
    created(){
        this.getList(); 
    }
}
</script>

<style scoped>
    .todoListContainer{
        width: 50%;
        margin: auto;
    }

    #title{
        background: #eeee;
        text-align: center;
        padding: 15px 0;
    }

    .addItem{
        text-align: center;
        padding: 15px 5px;
        background-color:#f6f6f6;
        color: rgb(26, 25, 22);
        font-size: 17px;
    }

    .listView{
        margin-top: 10px;
        padding: 15px 10px;
        background: #e8e8e8;
    }
</style>