<template>
  <div class="page">
    <header :class="theme === 'light' ? 'light-theme-back' : 'dark-theme-back'">
      <div class="container">
        <div class="d-flex justify-content-between align-items-center py-3">

          <a href="/" class="d-flex align-items-center justify-content-start link-dark text-decoration-none">
            <img src="/lab.png" alt="" style="width: 100px; height:100px">
          </a>

          <h1 class="justify-content-center">web2_11</h1>

          <div class="form-check form-switch justify-content-end">
            <input class="form-check-input input-size switch-input" type="checkbox" id="flexSwitchCheckDefault" @click="changeTheme">
            <label class="form-check-label switch-label" for="flexSwitchCheckDefault">Темная тема</label>
          </div>
        </div>
      </div>
    </header>

    <div :class="addNewPopup ? 'blur-div' : 'not-blur-div'">
      <div :class="theme === 'light' ? 'light-theme-main' : 'dark-theme-main'">
        <button class="add-button" :class="theme === 'light' ? 'light-theme-add-button' : 'dark-theme-add-button'" @click="showPopup()">Создать задачу</button>

        <div class="main-div">

          <div class="plan" @drop="onDrop($event, this.taskPlan)" @dragover.prevent @dragenter.prevent :class="theme === 'light' ? 'light-theme-column' : 'dark-theme-column'">
            <h3 style="text-align: center; margin-top: 10px">План ({{this.taskPlan.length}})</h3>
            <div :class="theme === 'light' ? 'light-theme-task-kard' : 'dark-theme-task-kard'" @dragstart="onDragStart($event, task, this.taskPlan)" draggable="true" v-for="task in taskPlan" :key="task[1]">
              <p class="importance" v-if="task[1]===1" style="background-color: red">{{task[1]}}</p>
              <p class="importance" v-if="task[1]===2" style="background-color: blue">{{task[1]}}</p>
              <p class="importance" v-if="task[1]===3" style="background-color: green">{{task[1]}}</p>
              <h3>Задача №{{this.taskPlan.indexOf(task) + 1}}</h3>
              <p>{{task[0]}}</p>
              <p>{{task[2]}}</p>
              <div class="navigation">
                <button :class="theme === 'light' ? 'light-theme-button-left-unactive' : 'dark-theme-button-left-unactive'">⇦</button>
                <button :class="theme === 'light' ? 'light-theme-edit-button' : 'dark-theme-edit-button'" @click="showEditPopup(task, this.taskPlan)">Edit</button>
                <button :class="theme === 'light' ? 'light-theme-button-right-active' : 'dark-theme-button-right-active'" @click="planToInWork(task)">⇨</button>
              </div>
            </div>
          </div>

          <div class="in-work" @drop="onDrop($event, this.taskInWork)" @dragover.prevent @dragenter.prevent :class="theme === 'light' ? 'light-theme-column' : 'dark-theme-column'">
            <h3 style="text-align: center; margin-top: 10px">В работе ({{this.taskInWork.length}})</h3>
            <div :class="theme === 'light' ? 'light-theme-task-kard' : 'dark-theme-task-kard'" @dragstart="onDragStart($event, task, this.taskInWork)" draggable="true"  v-for="task in taskInWork" :key="task[1]">
              <p class="importance" v-if="task[1]===1" style="background-color: red">{{task[1]}}</p>
              <p class="importance" v-if="task[1]===2" style="background-color: blue">{{task[1]}}</p>
              <p class="importance" v-if="task[1]===3" style="background-color: green">{{task[1]}}</p>
              <h3>Задача №{{this.taskInWork.indexOf(task) + 1}}</h3>
              <p>{{task[0]}}</p>
              <p>{{task[2]}}</p>
              <div class="navigation">
                <button :class="theme === 'light' ? 'light-theme-button-left-active' : 'dark-theme-button-left-active'" @click="inWorkToPlan(task)">⇦</button>
                <button :class="theme === 'light' ? 'light-theme-edit-button' : 'dark-theme-edit-button'" @click="showEditPopup(task, this.taskInWork)">Edit</button>
                <button :class="theme === 'light' ? 'light-theme-button-right-active' : 'dark-theme-button-right-active'" @click="inWorkToDone(task)">⇨</button>
              </div>
            </div>
          </div>

          <div class="done" @drop="onDrop($event, this.taskDone)" @dragover.prevent @dragenter.prevent :class="theme === 'light' ? 'light-theme-column' : 'dark-theme-column'">
            <h3 style="text-align: center; margin-top: 10px">Готово ({{this.taskDone.length}})</h3>
            <div :class="theme === 'light' ? 'light-theme-task-kard' : 'dark-theme-task-kard'" @dragstart="onDragStart($event, task, this.taskDone)" draggable="true" v-for="task in taskDone" :key="task[1]">
              <p class="importance" v-if="task[1]===1" style="background-color: red">{{task[1]}}</p>
              <p class="importance" v-if="task[1]===2" style="background-color: blue">{{task[1]}}</p>
              <p class="importance" v-if="task[1]===3" style="background-color: green">{{task[1]}}</p>
              <h3>Задача №{{this.taskDone.indexOf(task) + 1}}</h3>
              <p>{{task[0]}}</p>
              <p>{{task[2]}}</p>
              <div class="navigation">
                <button :class="theme === 'light' ? 'light-theme-button-left-active' : 'dark-theme-button-left-active'" @click="doneToInWork(task)">⇦</button>
                <button :class="theme === 'light' ? 'light-theme-edit-button' : 'dark-theme-edit-button'" @click="showEditPopup(task, this.taskDone)">Edit</button>
                <button :class="theme === 'light' ? 'light-theme-end-button' : 'dark-theme-end-button'" @click="deleteTask(task)">×</button>
              </div>
            </div>
          </div>

        </div>
      </div>
    </div>


        <div :class="theme === 'light' ? 'light-theme-addNewTask' : 'dark-theme-addNewTask'" v-if="addNewPopup">
          <div style="position: relative; height: 100%; width: 100%">
            <button :class="theme === 'light' ? 'light-theme-popup-button' : 'dark-theme-popup-button'" @click="closePopup()">X</button>
            <h5 :class="theme === 'light' ? 'light-theme-add-h' : 'dark-theme-add-h'">Описание</h5>
            <input type="text" v-model='description' :class="theme === 'light' ? 'light-theme-add-input' : 'dark-theme-add-input'">
            <h5 :class="theme === 'light' ? 'light-theme-h' : 'dark-theme-h'">Приоритет</h5>

            <select v-model="selectedItem" class="form-select" aria-label="Default select example" :class="theme === 'light' ? 'light-theme-select' : 'dark-theme-select'">
              <option value="1">Первый</option>
              <option value="2">Второй</option>
              <option value="3">Третий</option>
            </select>

            <button :class="theme === 'light' ? 'light-theme-popup-add-button' : 'dark-theme-popup-add-button'" @click="addNewTask()">{{this.buttonText}}</button>
          </div>
        </div>

    <footer :class="theme === 'light' ? 'light-theme-back' : 'dark-theme-back'">
      <h3>Крохалев Вячеслав Александрович 211-327</h3>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return{
      theme: "light",
      buttonText: "Добавить",
      addNewPopup: false,
      description: '',
      selectedItem: 1,
      taskId: [],
      taskPlan: [["Описание задачи", 3, "01.01.2022 14:14:14"], ["Описание задачи", 2, "01.01.2022 14:14:14"]],
      taskInWork: [["Описание задачи", 3, "01.01.2022 14:14:14"]],
      taskDone: [["Описание задачи", 1, "01.01.2022 14:14:14"]]
    }
  },
  methods: {
    onDrop(e, category){
      let categoryStart = e.dataTransfer.getData('categoryStart')
      let itemId = parseInt(e.dataTransfer.getData('itemId'))
      console.log(categoryStart)
      console.log(category.toString())
      if(category.toString() === this.taskDone.toString()){
        if(categoryStart === this.taskInWork.toString()){
          this.taskDone.push(this.taskInWork[itemId])
          this.taskInWork.splice(itemId, 1)
        }
        else if(categoryStart === this.taskPlan.toString()){
          this.taskDone.push(this.taskPlan[itemId])
          this.taskPlan.splice(itemId, 1)
        }
      }
      else if(category.toString() === this.taskInWork.toString()){
        if(categoryStart === this.taskDone.toString()){
          this.taskInWork.push(this.taskDone[itemId])
          this.taskDone.splice(itemId, 1)
        }
        else if(categoryStart === this.taskPlan.toString()){
          this.taskInWork.push(this.taskPlan[itemId])
          this.taskPlan.splice(itemId, 1)
        }
      }
      else if(category.toString() === this.taskPlan.toString()){
        if(categoryStart === this.taskDone.toString()){
          this.taskPlan.push(this.taskDone[itemId])
          this.taskDone.splice(itemId, 1)
        }
        else if(categoryStart === this.taskInWork.toString()){
          this.taskPlan.push(this.taskInWork[itemId])
          this.taskInWork.splice(itemId, 1)
        }
      }
    },
    onDragStart(e, item, category){
      e.dataTransfer.dropEffect = 'move'
      e.dataTransfer.effectAllowed = 'move'
      e.dataTransfer.setData('categoryStart', category.toString())
      e.dataTransfer.setData('itemId', category.indexOf(item).toString())
    },
    changeTheme(){
      this.theme = this.theme === "dark" ? "light" : "dark";
    },
    showEditPopup(task, group){
      if(this.addNewPopup === false){
        this.addNewPopup = true
      }
      this.buttonText = 'Редактировать'
      this.description = task[0]
      this.selectedItem = task[1]
      this.taskId = [group.indexOf(task), group]
    },
    addNewTask(){
      if(this.buttonText === "Добавить"){
        if (this.description.trim() !== ''){
          let dateTime = new Date()
          this.taskPlan.push([this.description, parseInt(this.selectedItem), `${dateTime.getDate()}.${String(dateTime.getMonth())}.${dateTime.getFullYear()} ${dateTime.getHours()}:${dateTime.getMinutes()}:00`])
          this.description = ''
          this.addNewPopup = false
        }
      }
      else if(this.buttonText === "Редактировать"){
        let group = this.taskId[1]
        let dateTime = new Date()
        group[this.taskId[0]] = [this.description, parseInt(this.selectedItem), `${dateTime.getDate()}.${String(dateTime.getMonth())}.${dateTime.getFullYear()} ${dateTime.getHours()}:${dateTime.getMinutes()}:00`]
        this.description = ''
        this.addNewPopup = false
      }
    },
    showPopup(){
      if(this.addNewPopup === false){
        this.addNewPopup = true
      }
      this.description = ''
      this.buttonText = 'Добавить'
    },
    closePopup(){
      if(this.addNewPopup === true){
        this.addNewPopup = false
      }
    },
    deleteTask(task){
      let indexTask = this.taskDone.indexOf(task)
      if (indexTask > -1){
        this.taskDone.splice(indexTask, 1)
      }
    },
    doneToInWork(task){
      let indexTask = this.taskDone.indexOf(task)
      if (indexTask > -1){
        this.taskDone.splice(indexTask, 1)
        this.taskInWork.push(task)
      }
    },
    inWorkToDone(task){
      let indexTask = this.taskInWork.indexOf(task)
      if (indexTask > -1){
        this.taskInWork.splice(indexTask, 1)
        this.taskDone.push(task)
      }
    },
    inWorkToPlan(task){
      let indexTask = this.taskInWork.indexOf(task)
      if (indexTask > -1){
        this.taskInWork.splice(indexTask, 1)
        this.taskPlan.push(task)
      }
    },
    planToInWork(task){
      let indexTask = this.taskPlan.indexOf(task)
      if (indexTask > -1){
        this.taskPlan.splice(indexTask, 1)
        this.taskInWork.push(task)
      }
    }
  }
}
</script>

<style>
.blur-div{
  filter: blur(5px);
  display: flex;
  flex: 2;
}
.not-blur-div{
  display: flex;
  flex: 2;
}

.dark-theme-popup-add-button{
  width: 30%;
  height: 30px;
  margin-left: 35%;
  margin-right: 35%;
  margin-top: 10%;
  border: blue thin;
  border-radius: 5px;
  color: white;
  background-color: darkblue;
}
.dark-theme-select{
  margin: 0 15% 0 15%;
  width: 70% !important;
  height: 40px;
  border-radius: 5px;
  color: white !important;
  background-color: blue !important;
}
.dark-theme-add-input{
  margin: 0 15% 0 15%;
  width: 70%;
  height: 40px;
  border-radius: 5px;
  border-color: blue;
  color: white !important;
  background-color: blue;
}
.dark-theme-add-h{
  padding-top: 15%;
  padding-left: 15%;
}
.dark-theme-h{
  padding-top: 5%;
  padding-left: 15%;
}
.dark-theme-popup-button{
  width: 25px;
  text-align: center;
  position: absolute;
  top: 10px;
  right: 10px;
  border-radius: 50%;
  border: darkblue solid thin;
  color: white;
  background-color: blue;
}
.dark-theme-addNewTask{
  position: absolute;
  width: 550px;
  height: 400px;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  margin: auto;
  background-color: darkgray;
  color: darkblue;
  border: darkblue solid;
}
.light-theme-popup-add-button{
  width: 30%;
  height: 30px;
  margin-left: 35%;
  margin-right: 35%;
  margin-top: 10%;
  border: lightblue thin;
  border-radius: 5px;
  color: white;
  background-color: blue;
}
.light-theme-select{
  margin: 0 15% 0 15%;
  width: 70% !important;
  height: 40px;
  border-radius: 5px;
  color: blue !important;
  background-color: lightblue !important;
}
.light-theme-add-input{
  margin: 0 15% 0 15%;
  width: 70%;
  height: 40px;
  border-radius: 5px;
  border-color: lightblue;
  color: blue !important;
  background-color: lightblue;
}
.light-theme-add-h{
  padding-top: 15%;
  padding-left: 15%;
}
.light-theme-h{
  padding-top: 5%;
  padding-left: 15%;
}
.light-theme-popup-button{
  width: 25px;
  text-align: center;
  position: absolute;
  top: 10px;
  right: 10px;
  border-radius: 50%;
  border: blue solid thin;
  color: blue;
  background-color: lightblue;
}
.light-theme-addNewTask{
  position: absolute;
  width: 550px;
  height: 400px;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  margin: auto;
  background-color: white;
  color: blue;
  border: blue solid;
}

.page{
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}
footer{
  margin-top: auto;
  text-align: center;
  padding: 10px;
}

.light-theme-back{
  background-color: blue;
  color: black !important;
}
.dark-theme-back{
  background-color: darkblue;
  color: white !important;
}

.switch-input{
  width: 60px !important;
  height: 30px !important;
  margin: 5px;
}
.switch-label{
  font-size: 20px;
  margin-top: 2px;
}

.light-theme-main{
  background-color: white;
  flex: 2;
}
.dark-theme-main{
  background-color: darkgray;
  flex: 2;
}
.light-theme-column{
  background-color: lightblue;
  color: black;
  border-radius: 10px;
}
.dark-theme-column{
  background-color: blue;
  color: white;
}

.add-button{
  margin-top: 50px;
  margin-left: 20%;
  height: 40px;
  width: 150px;
  border-radius: 10px;
  border: none;
  font-weight: bold;
}
.light-theme-add-button{
  background-color: blue;
  color: black;
}
.dark-theme-add-button{
  background-color: darkblue;
  color: white;
}

.main-div{
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  width: 100%;
}
.plan + .in-work + .done{
  display: flex;
  flex-direction: column;
}
.plan{
  margin: 30px 0 30px 10%;
  width: 22%;
  min-height: 60vh;
  position: relative;
}
.in-work{
  margin: 30px 5% 30px 5%;
  width: 22%;
  min-height: 60vh;
  position: relative;
}
.done{
  margin: 30px 10% 30px 0;
  width: 22%;
  min-height: 60vh;
  position: relative;
}

.light-theme-task-kard{
  margin: 10px;
  padding: 5px;
  border: medium solid blue;
  border-radius: 10px;
  background-color: white;
}
.dark-theme-task-kard{
  margin: 10px;
  padding: 5px;
  border: medium solid darkblue;
  border-radius: 10px;
  background-color: darkgray;
}

.importance{
  position: absolute;
  font-size: 15px;
  width: 20px;
  height: 22px;
  text-align: center;
  left: 90%;
  border-radius: 50%;
}

.navigation{
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin-bottom: 10px;
}
.light-theme-button-left-unactive{
  margin-left: 15px;
  width: 50px;
  height: 50px;
  border-radius: 15px;
  background-color: white;
  border-color: lightblue;
  color: lightblue;
  font-size: 30px;
}
.light-theme-button-left-active{
  margin-left: 15px;
  width: 50px;
  height: 50px;
  border-radius: 15px;
  background-color: lightblue;
  border-color: blue;
  color: blue;
  font-size: 30px;
}
.light-theme-edit-button{
  width: 50px;
  height: 50px;
  border-radius: 15px;
  background-color: lightblue;
  border-color: blue;
  color: blue;
}
.light-theme-button-right-active{
  margin-right: 15px;
  width: 50px;
  height: 50px;
  border-radius: 15px;
  background-color: lightblue;
  border-color: blue;
  color: blue;
  font-size: 30px;
}
.light-theme-end-button{
  margin-right: 15px;
  width: 50px;
  height: 50px;
  border-radius: 15px;
  background-color: lightblue;
  border-color: blue;
  color: blue;
  font-size: 30px;
}
.dark-theme-button-left-unactive{
  margin-left: 15px;
  width: 50px;
  height: 50px;
  border-radius: 15px;
  background-color: darkgray;
  border-color: blue;
  color: blue;
  font-size: 30px;
}
.dark-theme-button-left-active{
  margin-left: 15px;
  width: 50px;
  height: 50px;
  border-radius: 15px;
  background-color: blue;
  border-color: darkblue;
  color: darkblue;
  font-size: 30px;
}
.dark-theme-edit-button{
  width: 50px;
  height: 50px;
  border-radius: 15px;
  background-color: blue;
  border-color: darkblue;
  color: darkblue;
}
.dark-theme-button-right-active{
  margin-right: 15px;
  width: 50px;
  height: 50px;
  border-radius: 15px;
  background-color: blue;
  border-color: darkblue;
  color: darkblue;
  font-size: 30px;
}
.dark-theme-end-button{
  margin-right: 15px;
  width: 50px;
  height: 50px;
  border-radius: 15px;
  background-color: blue;
  border-color: darkblue;
  color: darkblue;
  font-size: 30px;
}
</style>
