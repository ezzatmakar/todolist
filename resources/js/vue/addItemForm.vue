<template>
    <div class="addItem">
        <input type="text" v-model="item.name" />
        <font-awesome-icon 
        icon="plus-circle" 
        @click="addItem()"
        :class="[ item.name ? 'active' : 'inactive' , 'plus']"
        />
    </div>
</template>

<script>
export default {
    data: function() {
        return {
            item: {
                name: ""
            }
        }
    }, methods: {
        addItem(){
            if(this.item.name == ''){
                return;
            } 
            axios.post('api/item/store', {
                item: this.item
            })
            .then( response => {
                if( response.status == 201){
                    this.item.name = "";
                    this.$emit('reloadlist');
                }
            })
            .catch( error => {
                 console.log(error);
            })
        }
    }
    
}
</script>

<style scoped>
.addItem {
    display: flex;
    justify-content: center;
    align-items: center;
}
input{
    padding: 7px;
    width: 92%;
    text-align: left;
}
svg{
    margin-left: 15px;
    text-align: right;
}

.plus{
    font-size: 20px;
}

.active{
    color: green;
}

.inactive{
    color:darkgray
}
</style>