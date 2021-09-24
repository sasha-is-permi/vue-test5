 <template>
  <div>
        <table >

        <div class="table-responsive">
        	<tbody>
           <div>

        		 <tr>
               <!-- При щелчке на заголовках генерируются события, которые будут обрабатываться в App -->
            <th @click="sortName">Имя</th>
            <th @click="sortTel">Телефон</th>
            <th @click="sortTel">Подчиненные сотрудники</th>
	         	</tr>     
              <tr  v-for="(item,index)  in table" :key="index" >                 
                <td> {{item.name}} </td>
                <td> {{item.tel}} </td>  
                  <table>    
                 <tr  v-for="(item2,index2)  in item.employee" :key="index2" > 
                   <td> {{item2.name}} </td>
                   <td> {{item2.tel}} </td>
                 </tr>
                 </table>

               </tr>
         </div>
      	</tbody>
        </div>
                     
         </table>
   <h2>Структура данных (для понимания тестового задания):</h2>
   {{table}} 

</div>


</template>

<script>
export default {
  name: 'ButtonComponent',
   props: ['table'],
  data () {
    return {

    }
  },
  methods:{
  sortName(){
     this.$emit('sortName',true)
  },
  sortTel(){
     this.$emit('sortTel',true)
}

  }
}
</script>

<style scoped>




table{
border-collapse:collapse;
border-spacing:0
}
table, td, th{
border: 1px solid #595959;
}
td, th{
padding: 20px;
width: 30px;
height: 25px;
}
th{
background-color: #7accee!important;
}

</style>

