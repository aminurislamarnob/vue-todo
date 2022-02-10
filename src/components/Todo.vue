<template>
    <div class="todos" v-if="todo" @click="$emit('toggleTodo')">
      <!-- Todo start -->
      <div class="todo" :class="{'todo--done': todo.status}">
        <div class="todo__status-dot"></div>
        <div>
          <p class="todo__content">{{ todo.title }}</p>
          <small class="todo__time"> {{ todo.date }} </small>
        </div>
      </div>
      <!-- Todo end -->
    </div>
</template>

<script>
export default {
    props: ["todo"],
}
</script>