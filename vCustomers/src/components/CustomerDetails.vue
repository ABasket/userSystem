<template>
    <div id="customerDetails container">
        {{customers}}
    </div>
</template>

<script>
  export default {
    name: 'customerDetails',
    data(){
      return{
        customers:""
      }
    },
    methods:{
      fetchCustomers(id){
        this.$http.get('http://localhost:3000/users/'+id).then(function (data) {
          this.customers = data.body;
        });
      }
    },
    created(){
      this.fetchCustomers(this.$route.params.id);
    }
  }
</script>

<style scoped>

</style>
