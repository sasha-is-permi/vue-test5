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
       
         let index= this.table.length  ; // определение индекса для  добавляемого в таблицу элемента. Он будет выполнять роль id
         console.log("index",index);

         this.form.id= index;        // новый индекс для  добавляемого в таблицу элемента. Он будет выполнять роль id
        // console.log("form1",this.form);         
         
          if ((typeof this.form.boss)=="string"){  // если у сотрудника нет начальника- добавляем полученные данные из form в таблицу
              let form1= {}
              form1.id= this.form.id; 
              form1.name= this.form.name;           // добавляем в таблицу нового сотрудника. У него нет сотрудников в подчинении
              form1.tel=  this.form.tel;            // (поле employees пустое)
              form1.employee="";

              this.table.push(form1);
          }
          else {   // Если есть начальник- добавляем к нему вновь добавившегося сотрудника из form
              let bossId = this.form.boss.id;
              let form = this.form;
            //  console.log("bossId",bossId);

              this.table.forEach(function(item) {
                  if(item.id === bossId){

                      console.log("item",item)
                      console.log("form",form)  
                      
                      item.employee={}
                      item.employee.id =  form.id
                      item.employee.name = form.name  
                      item.employee.tel = form.tel                      
                      item.employee.employee = ""

                      }
                      
              })

          }
         console.log("table1",this.table)   

       
    
    //   Объект сохранен в localStorage
       localStorage.setItem("table1",JSON.stringify(this.table))
    },
    sortName(){
       this.table.sort(function(a, b){
           let nameA=a.name.toLowerCase(), nameB=b.name.toLowerCase()
             if (nameA < nameB) //сортируем  по возрастанию
                return -1
             if (nameA > nameB)
             return 1
           return 0 // Никакой сортировки
            })
    },
    sortTel(){
       this.table.sort(function(a, b){
           let telA=a.tel, telB=b.tel
             if (telA < telB) //сортируем  по возрастанию
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