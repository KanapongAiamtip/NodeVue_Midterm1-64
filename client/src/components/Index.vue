<template>
  <div>
    <h1>Stock</h1>
    <div v-if="users.length">
      <h4>All Stock Short {{ users.length }}</h4>
      <p>
        <button v-on:click="navigateTo('/user/create')">
            Create stock
          </button>
      </p>
      <div v-for="user in users" v-bind:key="user.id">
        <p>id: {{ user.id }}</p>
        <p>Name of Short: {{ user.name }} - {{ user.lastname }}</p>
        <p>Details: {{ user.email }}</p>
        <p>Contact: {{ user.password }}</p>
        <p>
          <button v-on:click="navigateTo('/user/' + user.id)">
            Look All Data
          </button>
          <button v-on:click="navigateTo('/user/edit/' + user.id)">
            Edit Data
          </button>
          <button v-on:click="deleteUser(user)">
            Delete Data
          </button>
        </p>
        <hr />
      </div>
    </div>
  </div>
</template>
<script>
import UsersService from "@/services/UsersService";

export default {
  data() {
    return {
      users: [],
    };
  },
  async created() {
    try {
      this.users = (await UsersService.index()).data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteUser(user){
      let result = confirm("Want to delete")
      if(result){
        try{
          await UsersService.delete(user)
          this.refreshData()
        }catch(error){
          console.log(error)
        }
      }
    },
    async refreshData(){
      this.users = (await UsersService.index()).data
    }
  },
};
</script>
<style scoped>
</style>