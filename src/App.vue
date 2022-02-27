<template>
  <div id="app">

    <div class="todo-wrap">
      <span class="topBar">
        <span class="topBar-btn"/>
      </span>
      <div class="todoInput-wrap">
        <input type="text" id='todoInput' @input="changeInput" placeholder="Todos" @keyup.enter="add">
        <button type="submit" id="todoAdd-btn">+</button>
      </div>
      
      <ul class="todo-list">
        <li v-for="(todo, idx) in todos" :key="todo.todo + idx" :class="todo.compl === true ? 'done' : 'yet'"
          @click.stop="doneToggle($event)">
          {{ todo.todo }}
          <button class="todo-remove-btn" :data-id="todo.id" @click.stop="remove($event)" />
        </li>
      </ul>
    </div>

  </div>
</template>

<script>

export default{
  data(){
    return {
      todoInput : '',
      todos : [
        {
          id: 1,
          todo : 'Vue.js 학습하기',
          compl : false
        },

      ]
    }
  },
  methods : {
    changeInput(e) {
      this.todoInput = e.target.value;
    },
    add(e){
      if(e.target.value !== ''){
        const _id = this.todos.length+1;
        this.todos.push({ id: _id, todo : this.todoInput });
        this.todoInput = '';
        e.target.value = '';
      }
    },
    remove(e){
      const id = Number(e.target.dataset.id);
      this.todos.some((todo, index) => { 
        if(todo.id === id){
          this.todos.splice(index, 1);
        }
      });
    },
    doneToggle(e){
      const target = e.target;
      const isClass = e.target.classList.contains('yet');
      if(isClass){
        target.classList.replace('yet', 'done');
      }else{
        target.classList.replace('done', 'yet');
      }
    }
  }

}

</script>


<style>
*{
  box-sizing: border-box;
  margin: 0 auto;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background: #C6FFDD;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to right, #f7797d, #FBD786, #C6FFDD);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to right, #f7797d, #FBD786, #C6FFDD); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  position: relative;
  width: 100vw;
  height: 100vh;
}
.todo-wrap{
  display: flex;
  flex-direction: column;
  width: 400px;
  height: 600px;
  padding: 2.8rem 1rem 1rem 1rem;
  position: absolute;
  top: 50%; left: 50%;
  transform: translate(-50%, -50%);
  background: #e7e7e7;
  border-radius: 5px;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  overflow: hidden;
}
.topBar{
  position: absolute;
  top: 0; left: 0;
  width: 100%;
  height: 1.8rem;
  background: rgb(56, 53, 60);
  z-index: 100;
}
.topBar-btn{
  position: absolute;
  top: 50%; left: 10px;
  transform: translate(0, -50%);
  width: 0.9rem;
  height: 0.9rem;
  border-radius: 50%;
  background: rgb(238, 105, 94);
  cursor: pointer;
}
.topBar-btn::after{
  content: '';
  position: absolute;
  top: 50%; left: 22px;
  transform: translate(0, -50%);
  width: 0.9rem;
  height: 0.9rem;
  border-radius: 50%;
  background: rgb(246, 189, 79);
  cursor: pointer;
}
.topBar-btn::before{
  content: '';
  position: absolute;
  top: 50%; left: 44px;
  transform: translate(0, -50%);
  width: 0.9rem;
  height: 0.9rem;
  border-radius: 50%;
  background: rgb(97, 196, 84);
  cursor: pointer;
}
.todoInput-wrap{
  position: relative;
  width: 100%;
}

#todoInput{
  display: block;
  width: 100%; height: 2.4rem;
  padding: 0.4rem 2.8rem 0.4rem 0.6rem;
  font-size: 1rem;
  border: none;
  border-radius: 3px;
  background: #fff;
  outline: 0;
}
#todoAdd-btn{
  position: absolute;
  top: 0; right: 0;
  width: 2.4rem;
  height: 2.4rem;
  font-size: 1.5rem;
  color: #fff;
  background: #3581ff;
  border-radius:3px;
  outline: 0;
  border: none;
  cursor: pointer;
  transition: background 0.5s ease;
}
#todoAdd-btn:hover{
  background: #69a1ff;
}

.todo-list{
  display: block;
  list-style: none;
  width: 100%;
  height: 100%;
  background: #fff;
  margin: 1rem 0 0 0;
  padding: 0.4rem;
  border-radius: 3px;
  overflow: scroll;
}
*::-webkit-scrollbar-thumb{
  width: 2px;
}
.todo-list>li{
  position: relative;
  padding: 0.5rem 0.5rem 0.5rem 1.5rem;
  width: 100%;
  text-align: left;
  border-bottom: 1px solid rgb(242 242 242);
  cursor: pointer;
}
.todo-list>li.yet::after{
  content: '';
  position: absolute;
  top: 47%; left: 0.5rem;
  transform: translate(0, -50%);
  width: 6px; height: 1px;
  background: rgb(133, 133, 133);
  border-radius: 2px;
}
.done{
  text-decoration: line-through;
}

.todo-list>li.done::before{
  content: '';
  position: absolute;
  top: 46%; left: 0.4rem;
  transform: translate(0, -50%);
  width: 0.4rem; height: 0.4rem;
  border: 2px solid rgb(101, 150, 255);
  border-radius: 50%;
}

.todo-remove-btn{
  position: absolute;
  top: 50%; right: 5px;
  transform: translate(0, -50%);
  width: 1.7rem; height: 1.7rem;
  border-radius: 50%;
  border: 1px solid rgb(145, 145, 145); outline: 0;
  background: transparent;
  cursor: pointer;
}
.todo-remove-btn::after{
  content: '';
  position: absolute;
  top: 50%; left: 50%;
  transform: translate(-50%, -50%) rotate(45deg);
  display: inline-block;
  width: 1px; height: 50%;
  background: rgb(145, 145, 145);
  border-radius:2px;
}
.todo-remove-btn::before{
  content: '';
  position: absolute;
  top: 50%; left: 50%;
  transform: translate(-50%, -50%) rotate(135deg);
  display: inline-block;
  width: 1px; height: 50%;
  background: rgb(145, 145, 145);
  border-radius:2px;
}
</style>
