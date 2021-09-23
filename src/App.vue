<template>
  <div id="app">
    <ButtonComponent :isModalVisible="isModalVisible" @modalVisible="isModalVisible=$event" />            <!-- Компонент-кнопка -->
    <div id="space1">   </div>     <!-- Отступ от кнопки  --> 
    <div id="main">
      <!-- Передаем в дочерний компонент table объект table со значение таблицы
      Из таблицы ловим события sortName и sortTel и вызываем аналогичные функции этого модуля -->
       <TableComponent id="table" :table="table"   @sortName="sortName()"  @sortTel="sortTel()"      />  <!-- Компонент "таблица" -->
          <div id="space2">   </div>     <!-- Отступ от таблицы -->
        <!-- Слушаем событие "close" - если оно произошло в ModalComponent- isModalVisible=false (скрываем модальное окно)  
             Слушаем событие "onSubmit" - если оно произошло в ModalComponent- получаем от него данные формы (объект form)
             Передаем в ModalComponent массив объектов table и переменную isModalVisible
        -->  
       <ModalComponent :table="table"  :isModalVisible="isModalVisible" @close="isModalVisible=false" @onSubmit="form=$event; isModalVisible=false; addRow()"/>  <!-- Компонент "Диалоговое окно" -->
      
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
    
    //   Объект сохранен в localStorage
       localStorage.setItem("table1",JSON.stringify(this.table))
    },
    sortName(){
       this.table.sort(function(a, b){
           let nameA=a.name.toLowerCase(), nameB=b.name.toLowerCase()
             if (nameA < nameB) //сортируем строки по возрастанию
                return -1
             if (nameA > nameB)
             return 1
           return 0 // Никакой сортировки
            })
    },
    sortTel(){
       this.table.sort(function(a, b){
           let telA=a.tel, telB=b.tel
             if (telA < telB) //сортируем строки по возрастанию
                return -1
             if (telA > telB)
             return 1
           return 0 // Никакой сортировки
            })
    }, 
     setData() {                    
                 // Перебор уже существующих значений в localStorage 
    for(let i=0; i<localStorage.length; i++) {
 
    // Получаем по ключу записанный в localStorage объект
    let item = localStorage.getItem ( localStorage.key(i) );  
      
    let isJSON = true;
   
    try {
     JSON.parse(item);
    } catch (e) {
    //  console.log('строка не в формате JSON:',item);
      isJSON = false;
    }  

     // Если строка их хранища не в формате JSON- 
     // переходим на начало цикла, пропускаем данное значение
     if  (isJSON === false) continue;
      
     // А если в формате JSON- применяем функцию parse

     if  (localStorage.key(i)==="table1"){         
        this.table = JSON.parse(item);
          console.log('table',this.table);
            } 
    

  }                
                            }
  },
     // Считываем из localstorage записанный массив объектов table
     mounted() {
             this.setData();
      },

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