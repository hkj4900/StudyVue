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

    <v-content class = 'textField'>
      <input type = 'text' v-model="ToDoItem" placeholder="할 일을 입력해주세요">
      <v-btn @click="inputToDoItem">추가</v-btn>
      <p>{{this.ToDoList}}</p>
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
  width: 300px;
  left: 0;
  right: 0;
  margin-left: auto;
  margin-right: auto;
  margin-top: 15px;
}
</style>
