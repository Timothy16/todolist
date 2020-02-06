<template>
    <div>
        <div class="container mt-4">
        
     <h3><img src="favicon.ico" alt="" srcset="">CRUD operation using Vue JS</h3>  
          <hr> 
        </div>
     <div class="container back">    
  <div class="row">
    <div class="col-sm-8">
      <h2>List of registered Members</h2>
<table class="table border">
                      <thead>
                        <tr>
                          <th>S/N</th>
                          <th>Name</th>
                          <th>City</th>
                          <th>Role</th>
                          <th>Sex</th>
                          <th>Email</th>
                          <th>Actions</th>
                          
                        </tr>
                      </thead>
                      <tbody>
                      <tr v-for="(member, index) in members" :key="index">
                            
                          <td>{{index + 1}}</td>   
                          <td>{{member.name}}</td>
                          <td>{{member.city}}</td>
                          <td>{{member.role}}</td>
                          <td>{{member.sex}}</td>
                          <td>{{member.email}}</td>
                          <td>
                             <button class="btn btn-success ml"  @click="editUser(member)">
                                  Edit
                                </button>
                                <button class="btn btn-danger" @click="removeUser(index)">
                                  Delete
                                </button>
                               
                          </td>
                           
                        </tr>
                        </tbody>
                       
                  

</table>
 
      </div>   

<div class="col-sm-4">
  <h3>Not a member? fill the form below</h3>

<form @submit.prevent="addUser">
  <h3>Welcome {{newMembers.name}}</h3>
  <div class="form-group">
    <label>Name</label>
    <input type="text" v-model="newMembers.name" id="name" class="form-control" >
  </div>

  <div class="form-group">
    <label>City</label>
    <input type="text" v-model="newMembers.city" id="city" class="form-control">
  </div>

  <div class="form-group">
    <label>Role</label>
    <input type="text" v-model="newMembers.role" id="role" class="form-control">
  </div>


  <div class="form-group">
    <label>Email</label>
    <input type="text" id="score" class="form-control" v-model="newMembers.email">
  </div>
  
  

  <div class="form-group">
    <label>Sex:</label>
    <select class="form-control" v-model="newMembers.sex">
      <option disable selected>Please choose</option>
      <option value="male">Male</option>
      <option value="female">Female</option>
    </select>
  </div>
  
  <button v-if="status" type="submit" class="btn btn-primary">Submit</button>
  <button v-else type="click" class="btn btn-secondary ml-3" @click="updateUser">Update User</button>
  <button type="reset" class="btn btn-danger ml-3" id="reset">Reset</button>

</form>

    </div>
  </div>
 </div>

  <div class="container mt-3">
          
     <h5 style="text-align : center">&copy;Afolabi Timothy - Project Create 2.0</h5>
      
          <hr> 
    </div>

    </div>

    
</template>


<script>
import swal from 'sweetalert';
export default {
  data(){
    return{
      status : true,
        members : [
          {
            name : "Afolabi Timothy",
            city : "Lagos",
            role : "Web Developer",
            sex : 'male',
            email : "afolabi.timothy51@gmail.com",
          },

          {
            name : "Ekemini Anthony",
            city : "Uyo",
            role : "Vue Js Developer",
             sex : 'female',
            email : "kemzyyoung@gmail.com",
          },

          {
            name : "Mercy Mercy",
            city : "Eket",
            role : "Node Js",
             sex : 'female',
            email : "mercy53@gmail.com",
          }  
        ],
       
       newMembers : 
         {
            name : "",
            city : "",
            role : "",
             sex : "",
            email : "",
          },       
  } 
},
methods : {
    addUser(){

      if (this.newMembers.name === '' || this.newMembers.city === '' 
      || this.newMembers.role === '' || this.newMembers.sex === '' 
      || this.newMembers.email === '') {
        swal("Error!", "Field cannot be empty!", "error");
      }
      else if (this.newMembers.name === this.members.name 
      || this.newMembers.city === this.members.city  
      || this.newMembers.role === this.members.role  
      || this.newMembers.sex === this.members.sex  
      || this.newMembers.email === this.members.email ) {
        swal("Error!", "User Already Exist", "error");
      }
     
       else if(this.members.push(this.newMembers)) 
        swal("Successful! ", "You are now a member!", "success");
        },

    editUser(id){
       this.status = !this.status
       this.newMembers = id
        },
    removeUser(index){
      
       swal({
      title: "Are you sure?",
      text: "Once deleted, all information will be  lost!",
      icon: "warning",
      buttons: true,
      dangerMode: true,
})
      .then((willDelete) => {
        if (willDelete) {
          this.members.splice(index, 1)
          swal("Member successfully deleted!", {
            icon: "success",
          });
        } else {
          swal("You are still a member!");
        }
      });
    },
    updateUser(id){
      this.status = !this.status
      this.newMembers = id
     
    }
  },
  
}
</script>

<style scoped>
.back{
  background-color: lightgray;
}
</style>