<script setup>
 
import {useToast} from 'vue-toast-notification';
import axios from 'axios';
import { ref } from 'vue';

const props = defineProps ([ 'activeProduct']);
defineEmits(['update:activeProduct']);
const formData = ref({
ProductName : '',   
ProductCode : '',
Img : '',
Qty : '',
UnitPrice : '',
TotalPrice : '',
});

async function createProduct() {



   let url = "https://crud.teamrabbil.com/api/v1/CreateProduct";
   let data = await axios.post(url,formData.value);
   if(data.status == 200 && data.data.status == "success"){
      useToast().success('Product created successfully!');
    }else{
      useToast().error('Something went wrong!');
    }
}

</script>

<template>

    {{ props.activeProduct }}
   <h2 class="font-bold mt-20 mb-10" >Add a product</h2>
   <form @submit.prevent="createProduct()" class="p-8 bg-gray-100">
    <label for="ProductName">ProductName:</label><br>   
    <input class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" type="text" id="ProductName" v-model="formData.ProductName"><br> 
    <label  for="ProductCode">ProductCode:</label><br>   
    <input class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" type="text" id="ProductCode" v-model="formData.ProductCode"><br> 
    <label for="Img">Img:</label><br>
    <input class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" type="text" id="Img" v-model="formData.Img"><br>
    <label for="Qty">Qty</label><br>   
    <input class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" type="number" id="Description" v-model="formData.Qty"><br>
    <label  for="UnitPrice">UnitPrice:</label><br>
    <input class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" type="text" id="Price" v-model="formData.UnitPrice"><br>
    <label  for="TotalPrice">TotalPrice:</label><br>
    <input class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" type="text" id="Category" v-model="formData.TotalPrice"><br>
    <button type="submit" class="rounded-full bg-red-500 hover:bg-blue-700 text-white font-bold py-2 px-4  my-5" > Save changes</button>
   </form>
</template>

<style scoped></style>