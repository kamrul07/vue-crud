<script setup >
 import {useToast} from 'vue-toast-notification';
 import axios from 'axios';
 import { ref } from 'vue';

 defineProps ([ 'selectedProduct']);
 const emit = defineEmits(['update:selectedProduct']);

 function changeSelect(index){
    emit('update:selectedProduct',index);

 }

 const list = ref([]);

 getList();
 
 async function getList() {
    let url = "https://crud.teamrabbil.com/api/v1/ReadProduct";
    let data = await axios.get(url);
    list.value = data.data.data;
    
 }

 async function deleteProduct(id) {
    let url = "https://crud.teamrabbil.com/api/v1/DeleteProduct/"+id;
    let data = await axios.get(url);
    if(data.status == 200 && data.data.status == "success"){
       useToast().success('Product deleted successfully!');
     }else{
       useToast().error('Something went wrong!');
     }
    getList();
 }



</script>

<template>
    
    <notifications position="bottom right" classes="my-custom-class" />
  <h2>Product list</h2>
 <table class="table-auto border-separate border border-slate-400 ..." style="width:100%">
  <thead>
    <tr>
      <th class="border border-slate-300 ...">ID</th>
      <th class="border border-slate-300 ...">Name</th>
      <th class="border border-slate-300 ...">Product Code</th>
      <th class="border border-slate-300 ...">images</th>
      <th class="border border-slate-300 ...">Action</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="item , index in list" :key="index">
      <td class="border border-slate-300 ...">{{ item._id }}</td>
      <td class="border border-slate-300 ...">{{ item.ProductName }}</td>
      <td class="border border-slate-300 ...">{{ item.ProductCode }}</td>
      <td class="border border-slate-300 ..."><img :src="item.Img" alt=""></td>
      <td class="border border-slate-300 ...">
        <button @click="deleteProduct(item._id)" class="rounded-full bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4  my-5">Delete</button>
        <button @click="changeSelect(item._id)" class="rounded-full bg-red-500 hover:bg-blue-700 text-white font-bold py-2 px-4  my-5">Edit</button>
       </td>
    </tr>
  </tbody>
</table>

</template>

<style scoped></style>