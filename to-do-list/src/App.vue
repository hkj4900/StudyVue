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

    <v-content class = 'main-field' >
      <v-row style = "width: 100%">
        <input type = 'text' class = "input-field" v-model="ToDoItem" placeholder="할 일을 입력해주세요">
        <button class="button" @click="inputToDoItem">추가</button>
      </v-row>
      <v-row>
        <v-col>
          <h4>해야할 일</h4>
          <v-card  class="card-style" v-for="(item, i) in ToDoList" :key="i">
            <v-layout row>
              <v-layout col v-if="i != tempItemIndex" class="text-style" :cols = "10" @click="moveToCompleteList(item)">
                {{item}}
              </v-layout>
              <v-layout col v-else class="text-style" :cols = "10">
                <input type = 'text' placeholder="수정할 문구를 입력해주세요" v-model="tempItem">
              </v-layout>
              <v-layout col class="button-layout">
                <v-flex>
                  <v-layout row>
                    <v-flex>
                      <button v-if="i != tempItemIndex" dark class = "small-button" @click = "modifyToDoItem(i)" :disabled="modifySignal && i != tempItemIndex">수정</button>
                      <button v-else class = "small-button" @click = "confirmToDoItem(i)">확인</button>
                    </v-flex>
                  </v-layout>
                  <v-layout row>
                    <v-flex>
                      <button class = "small-button" @click = "deleteToDoItem(item)">삭제</button>
                    </v-flex>
                  </v-layout>
                </v-flex>
              </v-layout>
            </v-layout>
          </v-card>
        </v-col>
        <v-col>
          <h4>완료한 일</h4>
          <v-card class="card-style" v-for="(item, i) in completeList" :key="i">
            <v-row>
              <v-col class="text-style" :cols = "10" @click="moveToToDoList(item)">
                {{item}}
              </v-col>
              <v-col>
                <button class = "small-button" style="height: 40px" @click = "deleteCompleteItem(item)">삭제</button>
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
    completeList: [],
    modifySignal: false,
    tempItemIndex: '-1',
    tempItem: ''
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
    modifyToDoItem(i) {
      this.tempItem = this.ToDoList[i]
      this.tempItemIndex = i;
      this.modifySignal = !this.modifySignal
    },
    confirmToDoItem(i){
      if (this.tempItem !== '') {
        this.ToDoList[i] = this.tempItem
        this.tempItem = ''
      }
      this.tempItemIndex = -1;
      this.modifySignal = !this.modifySignal
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
.main-field{
  width: 70%;
  left: 0;
  right: 0;
  margin-left: auto;
  margin-right: auto;
  margin-top: 15px;
}
.input-field{
  width: 90%;
  height: 40px;
  border: solid;
  border-radius: 10px;
}
.button {
  width: 6%;
  height: 40px;
  background-color: lightgrey;
  border-radius: 10px;
  margin-left: 5px;
}
.small-button {
  font-size: 10px;
  background-color: lightgrey;
  border-radius: 10px;
  width: 10%;
  height: 20px;
}

.button-layout {
  position:absolute;
  left: 88%;
  bottom: 50%;
  transform: translate(0, 50%);
}

.card-style {
  width: 90%;
  margin-top: 13px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.text-style {
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
