  <template>
              <div class="row">
                <ul class="list-group mt-5">
                  <li v-for="(todo, index) in todos" :key="index" class="list-group-item">
                    <div class="row">
                      <div class="col">
                        <span v-if="todo.isDone">
                          {{ index+1 }}. {{ todo.activity }}<i class="bi bi-check-circle-fill text-success ms-2"></i>
                        </span>
                        <span v-else>
                          {{ index+1 }}. {{ todo.activity }}
                        </span>
                      </div>
                      <div class="col-auto">
                        <div class="row gx-2">
                          <div class="col">
                            <button @click="done(index)" class="btn btn-success align-content-end me-3"><i class="bi bi-check2-circle me-2"></i>Done</button>
                            <button @click="deleteTODO(index)" class="btn btn-danger align-content-end"><i class="bi bi-trash me-2"></i>Delete</button>
                          </div>
                        </div>
                      </div>
                    </div>
                  </li>
                </ul>
          </div>
  </template>

  <script>
  export default {
      props: {
        todos: {
          type: Array,
          default: [],
        }
      },
      setup(props, {emit}) {
          const deleteTODO = index => {
            emit('deleteTODO', index);
          }

          const done = index => {
            emit('done', index);
          }

          return {
            deleteTODO,
            done
          }
    },
  }
  </script>
