<template>
    <div class="item">
        <input
            type="checkbox"
            @change="updateCheck()"
            v-model="item.completed"
            />
            <span :class="[item.completed ? 'completed' : '', 'itemText']">{{ item.name }}</span>
            <button @click="removeItem()" class="trashcan">
                <font-awesome-icon icon="trash" />
            </button>
    </div>
</template>

<script>
export default {
    props: ['item'],
    methods: {
        updateCheck() {
            axios.put('api/item/' + this.item.id , {
                item: this.item
            })
            .then( response => {
                if( response.status == 200 ){
                    this.$emit('itmeChanged');
                }
            })
            .catch (error => {
                console.log( error );
            })
        },
        removeItem() {
            axios.delete('api/item/' + this.item.id )
            .then( response => {
                if( response.status == 200 ){
                    this.$emit('itmeChanged');
                    console.log(this.item.id + "item deleted succssefully")
                }
            })
            .catch (error => {
                console.log( error );
            })
        }
    }
}
</script>


<style scoped>
.completed{
    color: #ada5a5;
    text-decoration: line-through;
}
.itemText{
    width: 100%;
    margin-left: 20px;
}
.item{
    display: flex;
    justify-content: center;
    align-items: center;
}
</style> 