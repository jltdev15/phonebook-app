<template>
  <div>

    <!--     
    <p>Hi I am {{ name + ' ' + 'My age is ' + age }} </p>
    Dynamic Classes in Vue 3
    <button :class="disableAdd" :disabled="limitAge" @click="addAge" class="p-3 bg-blue-800 text-gray-50">Add
      Age</button>
    <button :class="disableMinus" :disabled="age <= 0" class="p-3 mx-3 bg-red-600 text-gray-50" @click="minusAge">Minus
      Age</button>
    <img :src="imgUrl" alt="">
    <div class="py-6">
      <button :class="{ active: isVueShow, 'bg-green-500': !isVueShow }" v-on:click="isVueShow = !isVueShow"
        class="inline-block p-3 mr-3 text-gray-50 rounded-2xl">{{
          isVueShow ? 'Hide' : 'Show' }}
        Vue</button>
      <button :disabled="!isVueShow" v-on:click="isVueShow = !isVueShow"
        class="inline-block p-3 bg-red-500 text-gray-50 rounded-2xl">Hide
        Vue</button>
      <div v-if="isVueShow">
        <p>Vue is easy to learn!!!</p>
      </div>
      <div v-else>
        <p>Vue is easier than react to learn</p>
      </div>
      <div v-show="isVueShow">
        <p>Vue is a progressive framework</p>
      </div>
      <div>
        <p>Reactive State Section</p>
        <p>Name: {{ person.name }}</p>
        <p>Age: {{ person.age }}</p>
        <button class="p-3 bg-blue-800 text-gray-50" @click="person.age++">Add age</button>
      </div>
    </div> -->
    <ul>
      <!-- <li v-for="(task, index ) in listOfTask" :key="task.id">
        {{ index }} - {{ task.name }}
      </li> -->
      <div v-if="checkTask">
        <li v-for="task in listOfTask" :key="task.id" class="flex justify-between"
          :class="{ 'bg-blue-600': task.isCompleted, 'bg-red-600': !task.isCompleted }">
          {{ task.name }}
          <button v-on:click="deleteTask(task.id)" class="bg-gray-200" v-if="task.isCompleted">Delete</button>
        </li>
      </div>
      <div v-else>
        <p class="text-center"> List of Task is Empty</p>
      </div>
      <div class="flex py-6">
        <input v-model="taskInput" type="text" class="border border-green-800">
        <button @click="addTask">Add Task</button>

      </div>
      <p>{{ taskInput }}</p>
    </ul>
  </div>
</template>


<!-- Composition Api Format -->
<script setup>
import { computed, ref, watch, reactive } from 'vue';

// Text Interpolation
// Ref State
const name = ref('John Lerry Taruc');
const age = ref(5)
const imgUrl = ref('https://resizing.flixster.com/wouDuoTzmfpwzvVDiTldrBHkbTo=/206x305/v2/https://resizing.flixster.com/8PNiwC2bpe9OecfYZSOVkvYC5vk=/ems.cHJkLWVtcy1hc3NldHMvbW92aWVzL2U5NGM0Y2Q1LTAyYTItNGFjNC1hNWZhLWMzYjJjOTdjMTFhOS5qcGc=')
const isVueShow = ref(false)
const taskInput = ref('')



// Reactive State

const person = reactive({
  name: 'John Lerry',
  age: 31
})

// V-for data
// List Rendering
const listOfTask = ref([
  {
    id: 1,
    name: 'Task number 1',
    isCompleted: true,

  },
  {
    id: 2,
    name: 'Task number 2',
    isCompleted: true,

  },
  {
    id: 3,
    name: 'Task number 3',
    isCompleted: true,

  }
])

const addTask = () => {
  const taskData = {
    id: 4,
    name: taskInput.value,
    isCompleted: false
  }
  listOfTask.value.push(taskData)
  taskInput.value = '';

}
const checkTask = computed(() => {
  return listOfTask.value.length;
})
const deleteTask = async (id) => {
  const data = listOfTask.value.filter((task) => task.id !== id)
  console.log(data);
  listOfTask.value = data;

}

// watch(age, (newValue, oldValue) => {
//   if (age.value >= 50) {

//     return age.value = 50
//   }
//   if (age.value <= 0) {

//     return age.value = 0
//   }
// })


// const limitAged = computed(() => {
//   if (age.value <= 0) {
//     return age.value = 0
//   }
//   if (age.value >= 50) {
//     return age.value = 50;
//   }
//   return age.value;

// })
const addAge = () => {
  age.value += 10;
}
const limitAge = computed(() => {
  return age.value >= 50
})

const disableAdd = computed(() => {
  if (age.value >= 50) {
    return 'bg-gray-200'
  }
  return ''
})
const disableMinus = computed(() => {
  if (age.value <= 0) {
    return 'bg-gray-200'
  }
  return ''
})

const minusAge = () => {
  age.value = age.value - 10;
}

console.log(limitAge.value);



</script>

<!-- Options API Format -->
<!-- <script>
export default {

  data() {
    return {
      name: 'John Lerry Taruc',
      age: 30,
    }
  },

}
</script> -->

<style>
.active {
  background-color: red;
}
</style>
