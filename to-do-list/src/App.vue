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

    <v-content class = 'mainField' >
      <input type = 'text' class = "inputField" v-model="ToDoItem" placeholder="할 일을 입력해주세요">
      <v-btn dark class="button" @click="inputToDoItem">추가</v-btn>
      <v-row>
        <v-col>
          <h4>해야할 일</h4>
          <v-card  class="cardStyle" v-for="(item, i) in ToDoList" :key="i">
            <v-row>
              <v-col class="textStyle" :cols = "10" @click="moveToCompleteList(item)">
                {{item}}
              </v-col>
              <v-col>
                <v-btn dark @click = "deleteToDoItem(item)">삭제</v-btn>
              </v-col>
            </v-row>
          </v-card>
        </v-col>
        <v-col>
          <h4>완료한 일</h4>
          <v-card class="cardStyle" v-for="(item, i) in completeList" :key="i">
            <v-row>
              <v-col class="textStyle" :cols = "10" @click="moveToToDoList(item)">
                {{item}}
              </v-col>
              <v-col>
                <v-btn dark @click = "deleteCompleteItem(item)">삭제</v-btn>
              </v-col>
            </v-row>
          </v-card>
        </v-col>
      </v-row>
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
    ToDoList: [],
    completeList: []
  }),
  methods: {
    inputToDoItem () {
      console.log(this.ToDoItem)
      console.log(this.ToDoList.length)
      let listIndex = this.ToDoList.length
      this.ToDoList[listIndex] = this.ToDoItem
      this.ToDoItem = ''
    },
    deleteToDoItem(item) {
      var index = this.ToDoList.indexOf(item);
      this.ToDoList.splice(index, 1);
    },
    deleteCompleteItem(item) {
      var index = this.completeList.indexOf(item);
      this.completeList.splice(index, 1);
    },
    moveToCompleteList(item) {
      this.deleteToDoItem(item)
      this.completeList.push(item)
    },
    moveToToDoList(item) {
      this.deleteCompleteItem(item)
      this.ToDoList.push(item)
    }
    
  }
};
</script>

<style scoped>
.mainField{
  width: 70%;
  left: 0;
  right: 0;
  margin-left: auto;
  margin-right: auto;
  margin-top: 15px;
}
.inputField{
  width:90%;
  height: 40px;
  border: solid;
  border-radius: 10px;
}
.button {
  margin-left: 5px;
  min-width: 20%;
  max-width: 20%;
  min-height: 40px;
  max-height: 40px;
}
.cardStyle {
  width: 90%;
  margin-top: 13px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.textStyle {
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
}
h4{
  width: 90%;
  text-align: center;
}
</style>
