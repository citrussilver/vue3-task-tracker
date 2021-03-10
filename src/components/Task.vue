<template>
  <div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder' : '', 'task']">
      <h3>
          {{task.text}}
          <i @click="$emit('delete-task', task.id)" class="fas fa-times"></i>
      </h3>
      <p>{{task.day}}</p>
  </div>
</template>

<script>
export default {
    name: 'Task',
    props: {
        task: Object,
    },
}
</script>

<style scoped>
.fas {
  color: red;
}
.task {
  margin: 5px;
  padding: 10px 20px;
  border-radius: .3em;
  cursor: pointer;
}
.task.reminder {
  border: 1px solid steelblue;
  border-radius: .3em;
  border-left: 5px solid green !important;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>