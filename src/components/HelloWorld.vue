<script setup>
import { ref, onMounted } from 'vue'

const imagesContainer = ref()
const intervalId = ref(null)
const delay = 5000
const numImages = 3
const idx = ref(0)
const show = ref(false)
const images = ref([
  'src/assets/img/img-01.jpg',
  'src/assets/img/img-02.jpg',
  'src/assets/img/img-03.jpg'
])

const generate = () => {
  console.log("generate", imagesContainer);
  imagesContainer.value.requestFullscreen()
}

onMounted(() => {
  console.log('onMounted')
  document.addEventListener("fullscreenchange", (ev) => {
    console.log('onfullscreenchange', { ev })
    show.value = !!document.fullscreenElement
    if (document.fullscreenElement) {
      console.log('fullscreen - enter')
      intervalId.value = setInterval(() => {
        console.log("Delayed for 1 second.", idx.value);
        idx.value = idx.value < (numImages - 1) ? idx.value + 1 : 0
      }, delay);
    } else {
      console.log('fullscreen - exit')
      clearInterval(intervalId.value);
      intervalId.value = null
    }
  })
})

</script>

<template>
  <main class="container">
    <h1 class="">Imágenes generadas por IA</h1>
    <button class="btn" @click="generate">Generar imágenes</button>
    <div v-show="show" class="images-container" ref="imagesContainer">
      <img class="image" :src="images[idx]" alt="">
    </div>
  </main>
</template>

<style scoped>
.container {
  margin: 0;
  display: flex;
  flex-direction: column;
  place-items: center;
}

.btn{
  align-items: center;
  background-color: #0066CC;
  border-radius: 50px;
  border: 2px solid #0066cc;
  box-shadow: rgb(0, 0, 0) 0px 0px 0px 0px;
  color: #fff;
  cursor: pointer;
  display: flex;
  flex-direction: row;
  font-family: Roboto, sans-serif;
  font-size: 40px;
  font-weight: 0;
  margin: 45px 0;
  padding: 30px 60px;
  transform: translateY(0);
  transition : 1000ms;
}

.btn:hover{
  background-color: #fff;
  border: solid 2px #0066cc;
  color: #0066cc;
  transform : translateY(-0px);
  transition : 600ms;
}

.images-container {
  background-color: #ffffff;
  /* min-height: 100vh; */
  display: flex;
  flex-direction: column;
  place-items: center;
  object-fit: fill;
}

.image {
  height: 100%;
}
</style>
