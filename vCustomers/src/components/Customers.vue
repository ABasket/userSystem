<template>
  <div id="customers" class="container">
    <alert v-if="alert" v-bind:Alert="alert"></alert>
    <h1 class="page-header">用户管理系统</h1>
    <table class="table table-striped">
      <thead>
      <tr>
        <th>姓名</th>
        <th>电话</th>
        <th>邮箱</th>
        <th></th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="customers in customers">
        <td>{{customers.name}}</td>
        <td>{{customers.phone}}</td>
        <td>{{customers.email}}</td>
        <td><router-link class="btn btn-default" v-bind:to="'/customerdetails/'+customers.id">详情</router-link></td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  import Alert from './Alert'
  export default {
    name: 'customers',
    data () {
      return {
        customers: [],
        alert:''
      }
    },
    components: {
    Alert
  },
    methods:{
      fetchCustomers(){
        this.$http.get('http://localhost:3000/users').then(function (data) {
            this.customers = data.body;
        });
      }
    },
    created(){
      if(this.$route.query.alert){
        this.alert=this.$route.query.alert;

      }
      this.fetchCustomers();
    },
    updated(){
      this.fetchCustomers();
    }



  }
</script>

<style scoped>

</style>
