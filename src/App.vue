<script>
export default {
  data() {
    return {
      placeholderTask: 'Напишите задачу',
      header: 'Список задач',
      inputTask: '',
      tasksList: ['Купить хлеб', 'Заправить машину', 'Забрать детей из школы', 'Сделать зарядку', 'Покормить кота', 'Позвонить Маме', 'Изучить ReactJS', 'Покормить енота', 'Позвонить Папе', 'Вызвать такси', 'Заказать ролы'],
      tasksListCompleted: ['Помыть машину', 'Полить цветы']
    }
  },
  methods: {
    addTask() {
      if (this.inputTask !== '') {
        this.tasksList.push(this.inputTask)
        this.inputTask = ''
      }
    },
    compliteTask(index) {
      this.tasksListCompleted.push(this.tasksList[index])
      this.deleteTask(index)
    },
    returnTask(index) {
      this.tasksList.push(this.tasksListCompleted[index])
      this.deleteCompliteTask(index)
    },
    deleteTask(index) {
      this.tasksList.splice(index, 1)
    },
    deleteCompliteTask(index) {
      this.tasksListCompleted.splice(index, 1)
    }
  },
  computed: {
    counterTasksList() {
      return this.tasksList.length
    },
    countertasksListCompleted() {
      return this.tasksListCompleted.length
    }
  }
}
</script>


<template>

  <div class="main">


    <div class="addtask">
      <h1> {{header}}</h1>
      <div class="addtaskform">
        <input class="addtask__input" type="text" :placeholder="placeholderTask" v-model="inputTask"
          @keypress.enter="addTask" />
        <button class="addtask__button" type="submit" @click="addTask"> Добавить задачу</button>
      </div>
    </div>

    <div class="taskslist">
      <div class="title">
        Задач на выполнение: {{counterTasksList}}
      </div>
      <ul class="list" v-if="counterTasksList!==0">
        <li v-for="(note,index) in tasksList">
          {{index+1}}. {{note}}
          <i @click="compliteTask(index)" title="Залача выполнена" class="fa-sharp fa-solid fa-square-check"></i>
          <i @click="deleteTask(index)" title="Удалить задачу" class="fa-sharp fa-solid fa-trash-can"></i>
        </li>
      </ul>
      <div v-else>
        Список задач пуст
      </div>
    </div>

    <div class="completedtaskslist">
      <div class="title">
        Выполнено задач: {{countertasksListCompleted}}
      </div>
      <ul class="list" v-if="countertasksListCompleted!==0">
        <li v-for="(note,index) in tasksListCompleted">
          {{index+1}}. {{note}}
          <i @click="returnTask(index)" title="Вернуть задачу на выполнение"
            class="fa-sharp fa-solid fa-square-check"></i>
          <i @click="deleteCompliteTask(index)" title="Удалить задачу" class="fa-sharp fa-solid fa-trash-can"></i>
        </li>
      </ul>
      <div v-else>
        Выполненных задач нет
      </div>
    </div>

  </div>
</template>

<style>
.main {
  background-color: #ffffff;
  font-family: Verdana;
  color: #ffffff;
}

.addtaskform {
  border: 1px solid #ffffff;
  padding: 4px 20px 4px 24px;
  width: 60%;
  margin: 0 auto;
  height: 40px;
  background-color: #ffffff;
  border-radius: 3px;
  text-align: center;
}

.title {
  text-align: center;
  font-size: 20px;
}

.list {
  list-style-type: none;
}

.list i {
  padding: 3px;
}

.main {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 150px auto;
  grid-gap: 5px;
  grid-template-areas:
    "H H"
    "TL CTL";
}

.addtask {
  grid-area: H;
  text-align: center;
  background-color: #0707d5;
}

.addtask__input,
::placeholder {
  border: none;
  margin: 0;
  outline: none;
  font-style: italic;
  height: 30px;
  vertical-align: top;
  background-color: #ffffff;
  color: #0707d5;
  font-size: 15px;
  padding: 0 8px 0 0;
  width: 70%
}

.addtask__button {
  border: none;
  margin: 0;
  padding: 0;
  font-size: 15px;
  text-transform: uppercase;
  line-height: 30px;
  color: #0707d5;
  background-color: #ffffff;
  cursor: pointer;
  transition: color .2s;
}


.taskslist {
  grid-area: TL;
  background-color: #0707d5;
}

.completedtaskslist {
  grid-area: CTL;
  background-color: #0707d5;
}


@media screen and (max-width: 1100px) {


  .main {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 150px auto auto;
    grid-gap: 0px;
    grid-gap: 5px;
    grid-template-areas:
      "H"
      "TL"
      "CTL";
  }

  .addtaskform {
    width: 95%;
    padding: 4px 2px 4px 2px;
  }

  .addtask__input {
    width: 65%;
  }

  .addtask__button {
    border: none;
    margin: 0;
    padding: 0;
    font-size: 15px;
    text-transform: uppercase;
    line-height: 30px;
    color: #0707d5;
    background-color: #ffffff;
    cursor: pointer;
    transition: color .2s;
  }
}
</style>
