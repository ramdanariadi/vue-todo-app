<template>
  <div>
    <div id="new-todo-container">
      <input
        type="text"
        class="new-todo"
        @keyup.enter="addNewTodo"
        name="newtodo"
        v-model="newTodo"
        placeholder="what should you do.."
      />
    </div>
    <div id="todo-container">
      <div
        class="todo-item"
        v-for="(item, index) in todosTemp"
        :key="item.todo"
      >
        <div class="todo-group">
          <input type="checkbox" class="cek" v-model="item.active" />
          <div class="todo-name" v-if="!item.editing" @dblclick="editing(item)">
            {{ item.todo }}
          </div>
          <input
            name="new-todo"
            type="text"
            class="new-todo"
            v-model="item.todo"
            @blur="finishEditing(item)"
            @keyup.enter="$event.target.blur()"
            v-else
            v-focus
          />
        </div>
        <span class="delete-todo" v-on:click="removeTodo(index)">&times;</span>
      </div>
      <div id="button-action-container">
        <button class="btn btn-success" v-on:click="all">All</button>
        <button class="btn btn-success" v-on:click="notActivedTodos">
          Completed
        </button>
        <button class="btn btn-warning" v-on:click="activedTodos">
          Not Completed
        </button>
        <button class="btn btn-danger" v-on:click="clear">
          Clear Completed
        </button>
        <span class="todo-progress"
          >{{ progress }} of {{ countTodos }} Completed</span
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "todocontainer",
  data: () => {
    return {
      todos: [
        { todo: "item 1", active: true, editing: false },
        { todo: "item 2", active: false, editing: false }
      ],
      filterType: "all",
      newTodo: "",
      editTodo: ""
    };
  },
  computed: {
    todosTemp: function() {
      if (this.filterType == "not-completed") {
        return this.todos.filter(todo => {
          return !todo.active;
        });
      }
      if (this.filterType == "completed") {
        return this.todos.filter(todo => {
          return todo.active;
        });
      }

      return this.todos;
    },
    progress: function() {
      return this.todos.filter(todo => {
        return todo.active;
      }).length;
    },
    countTodos: function() {
      return this.todos.length;
    }
  },
  methods: {
    all: function() {
      this.filterType = "all";
    },
    activedTodos: function() {
      this.filterType = "not-completed";
    },
    notActivedTodos: function() {
      this.filterType = "completed";
    },
    removeTodo: function(index) {
      this.todos.splice(index, 1);
    },
    clear: function() {
      this.todos = this.todos.filter(todo => {
        return !todo.active;
      });
    },
    addNewTodo: function() {
      this.todos.push({
        todo: this.newTodo,
        active: false,
        editing: false
      });
      this.newTodo = "";
    },
    editing: function(item) {
      item.editing = true;
    },
    finishEditing: function(item) {
      item.editing = false;
    },
    toast: function() {
      alert();
    }
  },
  directives: {
    focus: {
      inserted: function(el) {
        el.focus();
      }
    }
  }
};
</script>

<style scoped>
#new-todo-container {
  display: flex;
  justify-content: center;
}
.new-todo {
  height: 28px;
  padding: 8px;
  font-size: 16px;
  border: solid 2px #969696;
  width: 92%;
}
.edit-todo {
  height: 16px;
  padding: 8px;
  font-size: 16px;
  border: solid 2px #969696;
  width: 100%;
}

.edit-todo:focus {
  outline: none;
}

#todo-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 16px;
  background-color: antiquewhite;
}

.todo-item {
  width: 94%;
  padding: 15px;
  background-color: cadetblue;
  margin: 10px 0;
  position: relative;
  display: flex;
  align-items: center;
}

.todo-name {
  color: #ffffff;
}

.todo-group {
  width: 95%;
  display: flex;
  align-items: center;
}

.todo-name {
  margin-left: 10px;
}

.cek {
  margin: 0;
  padding: 0;
  width: 20px;
}

.delete-todo {
  position: absolute;
  right: 0;
  margin-right: 10px;
  font-weight: bold;
}

.delete-todo:hover {
  cursor: pointer;
}

#button-action-container {
  display: flex;
  align-items: center;
  width: 94%;
  padding: 15px;
  border-top: 1px solid black;
  position: relative;
}

.todo-progress {
  position: absolute;
  right: 0px;
  margin-right: 10px;
  color: #000000;
}

.btn {
  padding: 8px;
  color: #ffffff;
  border-radius: 8px;
}

.btn-primary {
  background-color: #5282ba;
  background-color: #517cae;
}

.btn-success {
  background-color: #52baa1;
  border: 1px solid #5ccfb3;
}

.btn-warning {
  background-color: #f8c67d;
  border: 1px solid #e1b674;
}

.btn-danger {
  background-color: #f87d7d;
  border: 1px solid #e37272;
}
</style>
