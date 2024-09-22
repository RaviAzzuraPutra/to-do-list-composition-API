<template>
    <div class="container mt-3">
        <div class="card">
          <div class="card-body">
            <h4 class="card-title">
              SIMPLE TO-DO LIST APP 
            </h4>
            <div class="row mt-3">
              <div class="col-10">
                <input v-model="todo" type="text" class="form-control" @keyup.enter="add">
              </div>
              <div class="col-2">
                <button class="btn btn-dark" @click="add"><i class="bi bi-plus-lg me-2"></i>Tambah</button>
              </div>
            </div>
            <list :todos="list" @deleteTODO="deleteTODO" @done="done"/>
            <small>Total: {{ totalTODO }}</small>
            <small class="ms-4" disabled><i class="bi bi-check-circle-fill text-success"></i> is Done</small>
          </div>
        </div>
    </div>
</template>

<script>
import list from './components/list.vue';
import {ref, reactive, onMounted, computed, toRefs} from 'vue';

export default {
  setup() {
    const todo = ref("");
      const todos = reactive({
        list: [],
      });

       onMounted(() => {
        const items = localStorage.getItem('todos');
          todos.list = items ? JSON.parse(items) : [];
       });

       const totalTODO = computed(() => {
        return todos.list.length;
       });

       const add = () => {
        todos.list.unshift({
          activity: todo.value,
          isDone: false
        }),
        todo.value = "";
        saveToLocalStorage();
       }

       const deleteTODO = todoIndex => {
        todos.list = todos.list.filter((item, index) => {
          if (index != todoIndex) {
            return item
          }
        });
        saveToLocalStorage();
       }

       const done = todoIndex => {
        todos.list = todos.list.filter((item, index) => {
          if (index == todoIndex) {
            item.isDone = true
          }
          return item
        });
        saveToLocalStorage();
       }

       const saveToLocalStorage = () => {
        localStorage.setItem('todos', JSON.stringify(todos.list));
       }

       return{
        todo,
        ...toRefs(todos),
        totalTODO,
        add,
        deleteTODO,
        done
       }
  },
    components: {
      list
    },
}
</script>
