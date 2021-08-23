<template>
<div>
    <h1>Edit User</h1>
    <form v-on:submit.prevent = "editUser">
        <p>Name of Short: <input type="text" v-model="user.name"></p>
        <p>Name of Short 2: <input type="text" v-model="user.lastname"></p>
        <p>Detail: <input type="text" v-model="user.email"></p>
        <p>Contact: <input type="text" v-model="user.password"></p>
        <p><button type="submit">edit user</button></p>
    </form>
    <hr>
    <div>
        <p>Name of Short: {{user.name}}</p>
        <p>Name of Short 2: {{user.lastname}}</p>
        <p>Detail: {{user.email}}</p>
        <p>Contact: {{user.password}}</p>
    </div>
</div>
</template>
<script>import UsersService from '@/services/UsersService'

export default {
    data(){
        return{
            user:{
                name: '',
                lastname: '',
                email: '',
                password: '',
                status: 'active'
            }
        }
    },
    methods:{
        async editUser(){
            try{
                await UsersService.put(this.user)
                this.$router.push({
                    name: 'users'
                })

            }catch(error){
                console.log(error)
            }
        }
    }, 
    async created(){
        try{
            let userId = this.$route.params.userId
            this.user = (await UsersService.show(userId)).data
        }catch(error){
            console.log(error)
        }
    }
}
</script>
<style scoped>


</style>