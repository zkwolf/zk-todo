<template>
  <sidebar>
    <div>
      All
    </div>
    <div v-for="todoType in todoTypes">
      {{ todoType }}
    <div>
  </sidebar>
</template>

<script>
export default {
  props: {
    todoTypes: ''
  }
}
</script>

<style scoped>
sidebar {
  flex: 0 0 18rem;
  background-color: rgba(30, 144, 255, 0.9)
}
sidebar div {
  font-size: 1.6rem;
  line-height: 2;
  text-align: center;
  color: #fff;
}
</style>