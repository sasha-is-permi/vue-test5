<template>
  <div>
    <!-- Показываем эту форму только если была нажата кнопка. submit не будет по умолчанию перезагружать страницу -->
    <form v-if="isModalVisible" @submit.prevent="onSubmit">
       <fieldset> 
       <div class="header"> 
        <span id="header1"> Добавление пользователя </span>
        <button id="close" @click="close" > x </button>
        </div>  
           <div class="form-row">
           <label for="name">Имя</label>
           <input type="text" id="name" v-model="name">
          </div>
          <div class="form-row">
           <label for="tel">Телефон</label>
           <input type="tel" id="tel" v-model="tel">
           </div>

           <div class="form-row">
           <label for="boss">Начальник</label>

          <select v-model="selected" id="boss">
          <option v-for="(item,index) in table" v-bind:value="item" :key="index">
             {{ item.name }}
          </option>
          </select>
           <span>Выбрано: {{ selected }}</span>

           </div>

          <div class="form-row">

           <button class="button" type="submit" @click="onSubmit">Отправить</button>
          </div>        
          </fieldset> 
        </form>
            
  </div>
</template>

<script>
export default {
  name: 'ButtonComponent',
  // Принимаем переменные isModalVisible и массив объектов table как параметры из компонента App
   props: ['isModalVisible','table'],
  data () {
    return {
      name:"",
      tel:"",
      selected:""

    }
  },
  methods:{
         close() {
// Передаем событие "close" в родительский компонент App если нажата кнопочка закрытия диалогового окна
   this.$emit('close');
},
// Передаем событие "onSubmit" в родительский компонент App вместе с данными формы
         onSubmit(){
           let form= {name:this.name, tel:this.tel,boss:this.selected}
           this.$emit('onSubmit',form);
           console.log('form',form)
         }
  }
}
</script>

<style scoped>

.form-row {
  display: flex;
  justify-content: flex-start;
  padding: .5em 0 .5em 0;
}
.form-row > label {
padding: .5em 1em .5em 0;
  flex: 1;
}
.form-row > input {
  flex: 2;
}
.form-row > input,
.form-row > button {
  padding: .5em;
}


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

.header{
  display:flex;
  justify-content: space-between;
  margin-bottom:10px;
}

.header1{
 font-size: 16px;
}

fieldset{
  padding: 10px 20px 20px 20px;
}

</style>
