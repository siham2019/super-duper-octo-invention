<template>
  <div id="app">

        <h1> TODO LIST APP </h1>
                    
            <div id="flex">
                   <input id="text" type="text" @keyup.enter="addTodo()" placeholder="write what do you want to do ?" v-model="body">

                   <input v-if="todos"  type="checkbox" class="check" @change="(e)=>checkAll(e)">
            </div>
           
          <p v-if="err" class="err">{{err}}</p> 
           <div id="todo">
                
                 <div  v-if="todos">
                   
                    <div v-for="item in todos" :key="item.id" class="todo">

                            <input type="checkbox" class="check" :checked="item.checked" @change="(e)=>checked(item.id,e.target.checked)">

                             <p :class="{r:item.v}">{{item.body}}</p>
                              <button class="x" @click="()=>clearx(item.id)">x</button>
                    </div>

                </div> 
                 
                 <div v-else class="todo">
                    <h1>there is no todos for instance</h1>
                 </div>
                
                <div id="todo-button">

                       <div>
                          <button @click="clearAll()">clear all</button>
                           <button @click="clear()">clear</button>  
                       </div>  
            
                  </div>
           </div>

       

  </div>
</template>

<script>



export default {
  name:"App",
  data() {
    return {
      todos:null,
      body:"",
      err:null,
    }
  },
  methods:{
    clearAll(){
        this.todos=null
    },
    reInit(){
      
      let i = 0

      this.todos.forEach(e=>{
        e.id=i;
        i++
      })

    },
    clear(){
      

      this.todos=this.todos.filter(e=>e.checked==false)
        this.reInit()

    },
    clearx(id){
        let t=this.todos.filter(e=>e.id!=id)
        
         this.todos = t
        
          
       this.reInit()   
  
    },
    checkAll(e){
        this.todos.forEach(element => {
               this.checked(element.id,e.target.checked)
         });
      

    },
    checked(id,v){

        if(v) {
             this.todos[id].checked=true;
             this.todos[id].v=true
        }
        else{         
              
           this.todos[id].v=false
           this.todos[id].checked=false;
       
        }
     },
    addTodo(){
       if (this.body.trim().length===0) {
          
          this.err="you write nothing"
          setTimeout(() => {
            this.err=""
          }, 3000);
        }
        else{
              if(!this.todos) this.todos=[]

                 this.todos.push({
                   id:this.todos.length,
                   body:this.body,
                   checked:false,
                   v:false
                })
        }
        this.body=""
    }
  }
}
</script>


<style>
     .r{
       text-decoration:line-through ;
     }
      #flex{
        
        display: flex;
        justify-content: center;
      }
      
      .todo h1{
         text-align: center;
          color: grey;
      }
     .err{
       color: red;
     }
     body{
       background-color: rgb(51, 51, 94);
       color: white;
       text-align: center;
     }
     #app{
       width: 100%;
     }
     #text{
       background-color: rgb(20, 19, 31);
       border: none;
       outline: none;
       text-align: center;
       border-bottom: 1px solid salmon;
         width:400px;
         padding: 5px;
         height: 30px;
         color: white;
         border-radius: 10px;
     }
     
     .x:hover{
       cursor: pointer;
     } 
     .x{
       margin-left: auto;
       background-color: rgb(20, 19, 31);
       font-size: 1.5em;
       border: none;
       color: whitesmoke;
     }

     .check{
        width: 30px;
        height: 35px;
     }
      ::placeholder{
        color: rgb(228, 222, 222);
        text-align: center;
        font-size: 1.5em;
      }

      #todo-button button{
        background-color: rgb(20, 19, 31);
        border: none;
        color: tomato;
      }

      #todo-button button:hover{

          text-decoration: underline;
          cursor: pointer;
      }

     #todo-button{
       padding: 10px  10px 5px 10px;
       display: flex;
       justify-content: space-between;

     
     }
      .todo .check{
       margin-right: 10px;
      }
     .todo{
        display: flex;
        padding: 10px;
        border-bottom: 1px solid rgb(88, 85, 85);
     }
  
     #todo{

             margin-top: 20px;
       background-color: rgb(20, 19, 31);
       width: 600px;
       margin-left: auto;
       margin-right: auto;
     }


</style>
