<template>
  <div>
        <table >
            <tr class="th">
            <th >Имя</th>
            <th>Телефон</th>
          </tr>
         <div v-for="item in table" :key="item.name">
              <tr> 
                <td> {{item.name}} </td>
                <td> {{item.tel}} </td>
               </tr>
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

table {
   border: 1px solid grey;
    min-width: 300px;

}

.th {
   border: 1px solid grey;
    min-width: 300px;

}

</style>

