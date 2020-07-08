<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <h3>To Do List</h3>

      <v-spacer></v-spacer>
    </v-app-bar>

    <v-content class = 'textField' >
      <input type = 'text' style = "width:100%" v-model="ToDoItem" placeholder="할 일을 입력해주세요">
      <v-btn @click="inputToDoItem">추가</v-btn>
      <v-card style = "width: 100%; margin-top: 20px; height: 5%; display: flex; align-items: center; justify-content: center;" v-for="(item, i) in ToDoList" :key="i">{{item}}</v-card>
    </v-content>
  </v-app>
</template>

<script> 

export default {
  name: 'App',

  components: {
  },

  data: () => ({
    ToDoItem: '',
    ToDoList: []
  }),
  methods: {
    inputToDoItem () {
      console.log(this.ToDoItem)
      console.log(this.ToDoList.length)
      let listIndex = this.ToDoList.length
      this.ToDoList[listIndex] = this.ToDoItem
      this.ToDoItem = ''
    }
  }
};
</script>

<style scoped>
.textField{
  width: 70%;
  left: 0;
  right: 0;
  margin-left: auto;
  margin-right: auto;
  margin-top: 15px;
}
</style>
