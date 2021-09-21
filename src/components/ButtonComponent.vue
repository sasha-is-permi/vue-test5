<template>
  <div>
    <button class="button" @click="modalVisible"> Добавить </button>
  </div>
</template>

<script>
export default {
  name: 'ButtonComponent',
  // Принимаем переменную isModalVisible как параметр из другого компонента
  props: ['isModalVisible'],
  data () {
    return {   
    }
  },
  methods: {
    modalVisible() {
// Передаем по событию modalVisible (слушаем его из других компонентов)
   this.$emit('modalVisible',true)
}
  }
}
</script>

<style scoped>
.button {
  cursor: pointer;
  border: 1px solid black;
  background: rgb(248, 248, 248);
  color: black;
  font-size: 16px;
  font-family: sans-serif;
  padding: 10px;
  border-radius: 50px 50px 50px 50px;

}
</style>
