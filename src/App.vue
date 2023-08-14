<script setup>
import { ref, reactive, onMounted, onBeforeUnmount, nextTick } from 'vue'
function reloadPage(){
  location.reload()
}
const items = ref([
    {
        title:'Male a Awesome Desktop Setup for Developer',
        url:'https://images.unsplash.com/photo-1619597455322-4fbbd820250a?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80'
    },
    {
        title:'Eius provident impedit cum! Tempore ex facere quae.',
        url:'https://images.unsplash.com/photo-1593640495253-23196b27a87f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1332&q=80'
    },
    {
        title:'Lorem ipsum dolor sit amet consectetur adipisicing elit.',
        url:'https://images.unsplash.com/photo-1493246507139-91e8fad9978e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80'
    },
    {
        title:'Rem obcaecati magni velit, eaque, hic officia est nemo quis libero tempore doloribus commodi',
        url:'https://images.unsplash.com/photo-1594031245755-1ac99bbc7a3c?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80'
    },
])

let carousel = null

onMounted(() =>{
    carousel = new Flickity( '#carousel', {});
})

onBeforeUnmount(() => {
    carousel.destroy()
})

let newItem = reactive({
    title:'',
    url:''
})

function updateCarousel(){
    items.value.push(newItem)
    console.log(items)
    carousel.destroy()

    nextTick(() =>{
        carousel = new Flickity( '#carousel', {});
    })
}

</script>
<template>
      <div class="mx-auto items mt-10 " id="carousel">
        <div class="item" :style="`background-image:url(${item.url})`" v-for="(item, index) in items" :key="index">
            <p class="pl-12 pr-12 pt-80 text-white font-bold ">{{ item.title }}</p>
        </div>
    </div>  
    <form>
        <div class="grid gap-6 mb-6 mt-10 md:grid-cols-3">
        <div>
            <input v-model="newItem.url" type="text" id="color-name" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" required placeholder="Image URL">
        </div>
        <div>
            <input v-model="newItem.title" type="text" id="color-name" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" required placeholder="Title">
        </div>

        <div>
            <button @click.prevent="updateCarousel()" type="submit" class=" mr-4 text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Add to Carousel</button>
            <button @click="reloadPage()" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-4 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"> RELOAD PAGE
        </button>
        </div>  
              
        </div>
    </form>
  
</template>

<style scoped>
.items{
    width: 1000px;
    height:500px;
}

.item{
    width: 1000px;
    height: 500px;
    background-color: gray;
    background-size: cover;
}

</style>
