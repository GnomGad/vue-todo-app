<template>
  <div>
    <h2>Добавить
      <input type="text" v-model="text">
      <button class="btn__save" @click="addTodo">Добавить</button>
      
    </h2>
    <br>
    <h2>Список задач {{todoArray.length > 0? todoArray.length: ''}}</h2>
    <ul>
      <li 
      v-for="(todo,index) in todoArray"
      :key="index"
      >
      <div>
        <p @click="complete(index)">{{todo}}</p>
        <img @click="deleteTodo(0,index)" src="./assets/trash.svg" alt="">
      </div>
      
    </li>
      
    </ul>
  </div>
  <div>
    <h2>Завершено {{completeArray.length > 0? completeArray.length: ''}}</h2>
    <ul>
      <li 
      class="completed"
      v-for="(todo,index) in completeArray"
      :key="index"
      >
      <div>
        <p @click="unComplete(index)">{{todo}}</p>
        <img @click="deleteTodo(1,index)" src="./assets/trash.svg" alt="">
      </div>
    </li>
    </ul>
  </div>
  
</template>

<script>


export default {
  name: 'App',
  components: {
  },
  data(){
    return {
      text: '',
      todoArray: [],
      completeArray: []
    }
  },
  methods:{
    addTodo(){
      if(this.text.length > 0){
        this.todoArray.push(this.text.trim())
        this.text = ''
      }
    },
    deleteTodo(typeArr,index){
      if(typeArr === 0){
        this.todoArray.splice(index,1)
      }
      else{
        this.completeArray.splice(index,1)
      }
    },
    complete(index){
      this.completeArray.push(this.todoArray[index])
      this.todoArray.splice(index,1)
    },
    unComplete(index){
      this.todoArray.push(this.completeArray[index])
      this.completeArray.splice(index,1)
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  padding: 0px 150px;
}

h2 {

  border: 1px solid black;
  background: black;
  color: white;
  font-size:32px;
  text-align: left;
  padding-left: 10px;
}
img{
  width: 40px;
  height: 40px;
  cursor: pointer;
}
ul {
  list-style: none;
  padding: 10px;
  font-size: 24px;
  margin-bottom: 20px;
  text-align: left;
}

li{
  margin-bottom: 2px;
}

li > div {
  display: flex;
  align-items: center;
}

li > div > p {
  border: 1px solid black;
  border-radius: 0px 30px 30px 0px;
  background: #f2f2f2;
  cursor: pointer;
  padding: 4px;
}
.btn__red {
  margin-left:10px;
  background: red;
  color: white;
  border: 1px solid black;
  border-radius: 30px;
  padding: 18px;
  cursor: pointer;
}
.completed {
  text-decoration: line-through;
  color: #ccc;
}

input {
  border: 1px solid black;
  border-radius: 30px;
  padding: 15px;
  font-size: 24px;
  margin-left: 10px;
}
.btn__save{
  background: green;
  color: white;
  border: 1px solid black;
  border-radius: 30px;
  padding: 18px;
  cursor: pointer;
}
</style>
