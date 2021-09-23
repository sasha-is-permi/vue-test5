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
	         	</tr>     
              <tr  v-for="(item,index)  in table" :key="index" >                 
                <td> {{item.name}} </td>
                <td> {{item.tel}} </td>      
                 <td v-if="(typeof item.employee!=='string')"> {{item.employee.name}} </td>
                 <td v-if="(typeof item.employee!=='string')"> {{item.employee.tel}} </td>

               </tr>
         </div>
      	</tbody>
        </div>
         
         </table>

    

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

