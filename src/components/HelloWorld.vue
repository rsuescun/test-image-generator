<script setup>
import { ref, onMounted } from 'vue'

const imagesContainer = ref()
const intervalId = ref(null)
const delay = 8000
const numImages = 8
const idx = ref(0)
const show = ref(false)
const images = ref([
  'https://www.montessoricartagena.edu.co/apps/image-test/imagen-ia-01.jpg',
  'https://www.montessoricartagena.edu.co/apps/image-test/imagen-ia-02.jpg',
  'https://www.montessoricartagena.edu.co/apps/image-test/imagen-ia-03.jpg',
  'https://www.montessoricartagena.edu.co/apps/image-test/imagen-ia-04.jpg',
  'https://www.montessoricartagena.edu.co/apps/image-test/imagen-ia-05.jpg',
  'https://www.montessoricartagena.edu.co/apps/image-test/imagen-ia-06.jpg',
  'https://www.montessoricartagena.edu.co/apps/image-test/imagen-ia-07.jpg',
  'https://www.montessoricartagena.edu.co/apps/image-test/imagen-ia-08.jpg',
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
    <h1 class="">Artp-IAs</h1>
    <button class="btn" @click="generate">
      <span>En una mesa hay una piña,</span>
      <span>dos cebollas.</span>
      <span>Y se ven dos vasijas.</span>
    </button>
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
  padding: 30px;
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
  flex-direction: column;
  font-family: Roboto, sans-serif;
  font-size: 40px;
  font-weight: 0;
  margin: 45px 0;
  max-width: 640px;
  padding: 30px 60px;
  place-items: center;
  transform: translateY(0);
  transition : 1000ms;
  width: 100%;
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
  display: flex;
  flex-direction: column;
  object-fit: fill;
  place-items: center;
}

.image {
  height: 100%;
}
</style>
