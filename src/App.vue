<template>
  <div id="app">
    <h1>Http</h1>
    <div class="form-group">
      <label>UserName</label>
        <input class="form-control" type="text" v-model="user.username">
    </div>
    <div class="form-group">
      <label>Mail</label>
        <input class="form-control" type="text" v-model="user.mail">
    </div>
    <button class="btn btn-primary" @click="submit">Submit</button>
    <hr>
     <input class="form-control" type="text" v-model="node">
    <br></br>
     <button class="btn btn-primary" @click="fetchData">Get Data</button>
     <ul class="list-group-item" v-for="u in users">{{u.username}}--{{u.mail}}</ul>
  </div>
</template>

<script>


export default {
  data () {
    return {
      user:
      {
        username:'',
        mail:''
      },
      users:[],
      resource:{},
      node:'data'
    };
  },
  methods:{
    
    submit(){
    //   this.$http.post('data.json',this.user)
    //     .then(response =>{
    //       console.log(response);
    //     },error =>{
    //       console.log(error);
    //     });
      //this.resource.save({},this.user);
      this.resource.saveAlt(this.user);
      
    },
    fetchData(){
    //  this.$http.get('data.json')
    //     .then(response =>{
    //       
    this.resource.getData({node:this.node})
    .then(response =>{
         return response.json();
        })
          .then(data =>{
            const resultArray =[];
            for(let key in data){
              resultArray.push(data[key]);
            }
            this.users=resultArray;
          });   
  
       }
       
       },
       created(){
         const customActions ={
           saveAlt:{method:'POST',url:'alternative.json'},
           getData:{method:'GET'}
         }
         this.resource=this.$resource('{node}.json',{},customActions);
  }
}
</script>

<style>

</style>
