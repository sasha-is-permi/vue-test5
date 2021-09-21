<template>
  <div id="app">
    <ButtonComponent :isModalVisible="isModalVisible" @modalVisible="isModalVisible=$event" />            <!-- Компонент-кнопка -->
    <div id="space1">   </div>     <!-- Отступ от кнопки  --> 
    <div id="main">
      <!-- Передаем в дочерний компонент table объект table со значение таблицы -->
       <TableComponent id="table" :table="table"/>  <!-- Компонент "таблица" -->
          <div id="space2">   </div>     <!-- Отступ от таблицы -->
        <!-- Слушаем событие "close" - если оно произошло в ModalComponent- isModalVisible=false (скрываем модальное окно)  
             Слушаем событие "onSubmit" - если оно произошло в ModalComponent- получаем от него данные формы (объект form)
        -->  
       <ModalComponent :isModalVisible="isModalVisible" @close="isModalVisible=false" @onSubmit="form=$event; isModalVisible=false; addRow()"/>  <!-- Компонент "Диалоговое окно" -->
      
    </div>   
  </div>
</template>

<script>
import ButtonComponent from './components/ButtonComponent'
import TableComponent from './components/TableComponent'
import ModalComponent from './components/ModalComponent'

export default {
  name: 'App',
  components: {
    ButtonComponent,
    TableComponent,
    ModalComponent
  },
  data () {
    return {
      form:{},
      isModalVisible: false,
      table:[]
    }
  },
  methods:{
    addRow(){
        this.table.push(this.form);
    }
  }
}
</script>

<style scoped>
#app{
  margin-top: 50px; 
  margin-left:50px;
  

}

#space1{
 height: 50px;    
}

#space2{
 width: 50px;    
}

/* Если разрешение экрана >700px- блоки рядом, если меньше- друг под другом */
@media (min-width: 700px) {
#main{
  display:flex;
  justify-content:flex-start;
 
}
}

/* Если разрешение экрана <700px -  отступы между блоками */
@media (max-width: 699px) {
#table{
    margin-bottom: 20px; 
}
}



</style>