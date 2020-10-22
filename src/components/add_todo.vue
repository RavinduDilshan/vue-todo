<template>
    <div>
        <form @submit="add_todo">
            <input type="text" v-model="title" name="titile" placeholder="Add Todo....">
            <input type="submit" value="submit" class="btn">
        </form>
    </div>
</template>

<script>

export default {
    name:"add_todo",
    data(){
        return{
            title:''
        }
    },

    methods:{
        add_todo(e){
            e.preventDefault();
            const new_todo={
                id:Math.random(),
                title:this.title,
                completed:false
            }

            //send upto parents
            this.$emit('add-todo',new_todo);
            this.title='';
        }
    }
}
</script>
    
<style scoped>
    form {
        display: flex;
    }

    input[type="text"]{
        flex: 10;
        padding: 5px;
    }

    input[type="submit"]{
        flex: 2;
    }

</style>