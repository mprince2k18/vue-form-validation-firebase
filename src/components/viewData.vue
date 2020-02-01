<template>
<div>




  <table class="table">
    <thead>
      <tr>
        <th scope="col">#</th>
        <th scope="col">First</th>
        <th scope="col">Last</th>
        <th scope="col">Handle</th>
      </tr>
    </thead>
    <tbody>

      <tr v-for="user in users" v-bind:key="user">
        <th scope="row">{{ index++ }}</th>
        <td>{{ user.name }}</td>
        <td>{{ user.username }}</td>
        <td>{{ user.email }}</td>
      </tr>

    </tbody>
  </table>




</div>
</template>

<script type="text/javascript">

  export default{
    name:'viewData',
    data(){
      return {
        index: '',
        users:[]
      }
    },
    created(){
      this.$http.get('https://laravel-6ae0a.firebaseio.com/post.json').then(res =>{
        this.users = res.body;
      });
    },
  }

</script>

<style media="screen" scoped>

</style>
