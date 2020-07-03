<template>
  <div>
    <div class="container">
      <div class="row mt-4">
        <div class="col-md-4 col-sm-12 col-lg-4 col-xl-4 col-xxl-4">
          <div class="card">
            <div class="card-header">
              Crear Todo List
            </div>
            <div class="card-body">
              <form @submit.prevent="addTodo">
                <div class="form-group mb-4">
                  <input v-model="title" type="text" placeholder="Titulo del todo list" class="form-control">
                </div>
                <div class="form-group mb-4">
                  <textarea v-model="description" cols="30" rows="10" placeholder="Descriptición del todo list" class="form-control"></textarea>
                </div>

                <button class="btn btn-dark btn-block">Guardar Todo list</button>
              </form>
            </div>
          </div>
        </div>

        <div class="col-md-8 col-sm-12 col-lg-8 col-xl-8 col-xxl-8">
          <div class="card" v-for="todo in todos" :key="todo.id">
            <div class="card-body">
              <h5 class="card-title" @dblclick="editTodoTitle" v-show="!editingTitle">{{ todo.title }}</h5>
              <div class="form-group">
                <input type="text" v-model="todo.title" v-show="editingTitle" @keyup.enter="saveEditTitle()" class="form-control">
              </div>
              
              <p class="card-text" @dblclick="editTodoDescription" v-show="!editingDescription">{{ todo.description }}</p>
              <div class="form-group">
                <input type="text" v-model="todo.description" v-show="editingDescription" @keyup.enter="saveTodoDescription()" class="form-control">
              </div>

              <button class="color-danger" @click="deleteTodo">
                <svg width="2em" height="2em" viewBox="0 0 16 16" class="bi bi-trash" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
                  <path d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z"/>
                  <path fill-rule="evenodd" d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4L4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z"/>
                </svg>
              </button>
              <button class="color-success">
                <svg width="2em" height="2em" viewBox="0 0 16 16" class="bi bi-pencil" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" d="M11.293 1.293a1 1 0 0 1 1.414 0l2 2a1 1 0 0 1 0 1.414l-9 9a1 1 0 0 1-.39.242l-3 1a1 1 0 0 1-1.266-1.265l1-3a1 1 0 0 1 .242-.391l9-9zM12 2l2 2-9 9-3 1 1-3 9-9z"/>
                  <path fill-rule="evenodd" d="M12.146 6.354l-2.5-2.5.708-.708 2.5 2.5-.707.708zM3 10v.5a.5.5 0 0 0 .5.5H4v.5a.5.5 0 0 0 .5.5H5v.5a.5.5 0 0 0 .5.5H6v-1.5a.5.5 0 0 0-.5-.5H5v-.5a.5.5 0 0 0-.5-.5H3z"/>
                </svg>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      description: '',
      todos: [],
      editingTitle: false,
      editingDescription: false
    }
  },

  methods: {
    addTodo() {
      this.todos.unshift({
        title: this.title,
        description: this.description
      })

      this.title = '';
      this.description = '';
    },

    deleteTodo(index) {
      this.todos.splice(index, 1);
    },

    editTodoTitle() {
      this.editingTitle = true;
    },

    saveEditTitle() {
      this.editingTitle = false;
    },

    editTodoDescription() {
      this.editingDescription = true;
    },

    saveTodoDescription() {
      this.editingDescription = false;
    }

  }
}
</script>

<style scoped>
  .color-danger {
    color: #b71c1c;
  }

  .color-success {
    color: #1a237e;
  }
</style>