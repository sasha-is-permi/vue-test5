 <template>
  <div>
        <table >

        <div class="table-responsive">
        	<tbody>
           <div>

        		 <tr>
            <th >Имя</th>
            <th>Телефон</th>
	         	</tr>     
              <tr  v-for="(item,index)  in table" :key="index" > 
                <td> {{item.name}} </td>
                <td> {{item.tel}} </td>                
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

