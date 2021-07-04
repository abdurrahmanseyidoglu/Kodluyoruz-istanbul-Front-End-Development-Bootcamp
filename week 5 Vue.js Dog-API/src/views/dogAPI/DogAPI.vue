<template>

  <div class="dog"> 
  <ul class="dog__ul">
      <li class="dog__li" v-for="(value, name) in data.message" :key="name"
      @click="fetchAPI()" 
      >
      {{ name }} 
      </li>
  </ul>
    <img :src="image"  alt="dog picture" class="dog__img"> 
  </div> 
</template> 
 
<script>
import { ref , onMounted, onUnmounted } from 'vue';
export default { 
 
  setup(){
    const data = ref({});
    let image = ref(null);
    
    function  fetchList(){ 
      fetch("https://dog.ceo/api/breeds/list/all")
        .then(response => response.json()) 
        .then(info=>data.value = info)
        .catch(err => console.log (err.message))
    }
      function fetchAPI(){ 
      fetch(`https://dog.ceo/api/breeds/image/random`)
        .then(response => response.json()) 
        .then(val=>image.value = val.message)
        .catch(err => console.log (err.message))
    }
    onMounted(() => {
      console.log ("Mount : DogAPI  Mounted ⭕");
      fetchAPI() 
      fetchList(); 
       
    });
    onUnmounted(() => console.log("unMount: DogAPI Unounted ❌ "));
    return {
      data,
      image,
      fetchAPI,
      
    }
  }
  
}; 
</script>
<style lang="scss">
.dog {
display: flex;
flex-direction:column;
align-items: center;
justify-content: center;
  &__img{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border-radius: 10px;
    height: 400px;
    width: 400px;
  }
  &__ul {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
    gap: 10px;
    list-style-type: none;

  }
  &__li{
      border: orchid dashed;
      padding: 3px;
      background-color: aqua;
      &:hover{
        background-color: pink;
        cursor: pointer;
      }
    }
  
  
  
}
</style>

