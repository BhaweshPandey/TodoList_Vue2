<template>
  <div class="columns is-multiline">
    <div class="column is-6 is-offset-3">
      <div class="box">
        <form @submit.prevent="onSubmit">
          <div class="field">
            <label class="label">Add Your Todo</label>
            <div class="control">
              <input class="input" v-model="name" type="text" placeholder="Enter Your todo.." />
            </div>
          </div>
        </form>
      </div>
    </div>
    <div class="column is-6 is-offset-3" v-for="(item, i) in todos" :key="i">
      <div class="box todo_box">
        <span >{{ item.name }}</span>
        <button class="button is-danger is-small is-pulled-right" @click="$emit('onDelete', item.id)">Delete</button>
      </div>
    </div>
  </div>
</template>

<script>
import shortid from 'shortid'
export default {
  name: 'TodoItem',
  props: ["todos"],
  data() {
    return {
      name: ''
    }
  },
  methods: {
    onSubmit() {
      const new_todo = {
        name: this.name,
        id: shortid.generate()
      };
      this.$emit("addTodo", new_todo);
      this.name = "";
    },
  },
};
</script>

<style>
.completd {
  text-decoration: line-through;
}

.todo_box {
  transition: all 0.3;
}

.todo_box:hover {
  cursor: pointer;
  background-color: red;
  transform: scale(1.1);

}
</style>