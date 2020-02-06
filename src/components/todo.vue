<template>
    <div>
             <div class="container mt-4">
        
     <h3><img src="favicon.ico" alt="" srcset="">Todo-list using Vue Js</h3>  
          <hr> 
        </div>
        
        <div class="container mt-4 head">
          <center><h3><img src="m3.png" alt="" srcset="" width="100" height="100"> <br> Welcome, it's {{date()}}</h3></center>    
        <div class="row">
            <div class="col-sm-2 ">
                
                   
                    <form >
  
            <div class="form-group">
                <label>Project/Task:</label>
                <input type="text"  class="form-control" v-model="newTodo.project">
            </div>

            <div class="form-group">
                <label>Categories:</label>
                <select class="form-control" v-model="newTodo.categories">
                <option disable selected>Please choose</option>
                <option value="Business">Business</option>
                <option value="Personal">Personal</option>
                 <option value="Family">Family</option>
                <option value="Career">Career</option>

                </select>
            </div>

             <div class="form-group">
                <label>Priority:</label>
                <select class="form-control" v-model="newTodo.priority">
                <option disable selected>Please choose</option>
                <option value="High Priority"><img src="@/assets/icons/plus.svg" alt="e" width="30" height="30" title="" >High Priority</option>
                <option value="Low Priority">Low Priority</option>
                

                </select>
            </div>

            <div class="form-group" >
                <label for="comment">Description:</label>
                
                <textarea class="form-control" rows="5" id="comment" v-model="newTodo.description"></textarea>
                </div>


            <div class="form-group">
                <label>Date:</label>
                <input type="text"  class="form-control" v-model="newTodo.date">
            </div>

             <div class="form-group">
                <label>Time:</label>
                <input type="text"  class="form-control" v-model="newTodo.time">
            </div>

                     <button v-if="update" class="btn btn-success btn-sm" type="submit" @click.prevent="addUser"> Add To-do 
                         <img src="@/assets/icons/plus.svg" alt="e" width="50" height="30" title="" ></button>
                         <button v-else class="btn btn-dark btn-sm" type="click" @click.prevent="updateUser(index)">Update</button>
                    <button class="btn btn-secondary ml-2 mt-1 btn-sm" type="reset"> Reset</button>
            
          </form>  

           


            </div>

            <div class="col-sm-10 mt-3">
                
<table class="table border">
                      <thead>
                        <tr>
                          <th>S/N</th>
                          <th>Todo</th>
                          <th>Categories</th>
                          <th>Priority</th>
                          <th>Description</th>
                          <th>Date</th>
                          <th>Time</th>
                          <th>Status</th>
                          <th>Action</th>
                          
                        </tr>
                      </thead>
                      <tbody>
                      <tr v-for="(todo, index) in todos" :key="index">
                            
                          <td>{{index + 1}}</td>   
                          <td>{{todo.project}}</td>
                          <td>{{todo.categories}}</td>
                          <td>{{todo.priority}}</td>
                          <td>{{todo.description}}</td>
                          <td>{{todo.date}}</td>
                          <td>{{todo.time}}</td>
                          <td>
                             
                              <button v-if="status" class="btn btn-success btn-sm">
                                  Completed
                                </button>
                                <button v-else class="btn btn-danger btn-sm" >
                                  Pending
                                </button>
                              <center>
                                  
                              <div class="form-check">
                                <label class="form-check-label">
                                    <input type="checkbox" class="form-check-input" value=""  @click="toggleOn(index)">
                                </label>
                                </div> </center><br>
                               
                                
                          </td>
                          <td>
                             <button  class="btn btn-success btn-sm" @click="editUser(todo)">
                                 <img src="@/assets/icons/check.svg" alt="e" width="30" height="30" title="" >
                                </button>
                                <button class="btn btn-danger btn-sm " @click="removeUser(index)">
                                   <img src="@/assets/icons/x-circle.svg" alt="e" width="30" height="30" title="" >
                                </button>
                               
                          </td>
                           
                        </tr>
                        </tbody>
                       
                  

</table>
            </div>
        </div>
     
        </div>
    </div>
</template>


<script>
import swal from "sweetalert"

export default {
    data(){

        return{
        status : false,
        update : true,
        todos: [
          {
            project: "Travel",
            categories: "Personal",
            priority : "High Priority",
            description : 'Flight to Lagos',
            date : "12-03-12",
            time : "11:00am"
          },
         ],

         newTodo :{
            project: "",
            categories: "",
            priority : "",
            description : '',
            date : "",
            time : ""
         }
        }
    },
    methods : {
        addUser(){
            if (this.newTodo.project === '' || this.newTodo.categories === '' 
      || this.newTodo.priority === '' || this.newTodo.description === '' 
      || this.newTodo.date === '' || this.newTodo.time === '') {
        swal("hoops!", "No Todo to add!", "warning");
      }
           else if(this.todos.push(this.newTodo)) {
                swal("Successful! ", "To-do list added!", "success")
           }
            
           
        },
       
    removeUser(index){
      
       swal({
      title: "Are you sure?",
      text: "Once deleted, task will be  lost!",
      icon: "warning",
      buttons: true,
      dangerMode: true,
})
      .then((willDelete) => {
        if (willDelete) {
          this.todos.splice(index, 1)
          swal("Todo successfully deleted!", {
            icon: "success",
          });
        } else {
          swal("Todo still available!");
        }
      });
            
        },
    
    toggleOn(index){
        this.status = !this.status
        
    },

    editUser(id){
        this.update = !this.update
        this.newTodo = id
    },

    updateUser(index){
        this.todos.push(index)
    },

     date(){
            let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
            //  return (new Date().getDate())
            let day = days[new Date().getDay()]
            return day
        }

    }

}
    // methods : {
    //      date(){
    //     let today 
    //     let dd = String(today.getDate()).padStart(2, '0');
    //     let mm = String(today.getmonth() + 1).padStart(2, '0');
    //     let yyyy= today.getFullYear();

    //     today = mm + '/' + dd + '/' + yyyy;
    //     return today
    // }
    
   
    

</script>>

<style scoped>
.head{
    background-color: lightseagreen;
}
</style>