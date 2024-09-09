<script setup>
import { ref, onMounted } from 'vue'
import Person from './components/Person.vue'
import Message from './components/Message.vue'

const mensajes = ref([])

</script>

<template>
  <Person @saveMessage="(msg) => mensajes.push(msg)" alineacion="izquierda" />
  <div 
  class="chat">
    <Message v-for="(mensaje, i) in mensajes" :key="i" :mensaje="mensaje">
      {{ mensaje.texto }}
    </Message>
  </div>
  <Person @saveMessage="(msg) => mensajes.push(msg)" alineacion="derecha" />
</template>

<style scoped>
.chat {
  background-color: gainsboro;
  box-shadow: 0 0 2px 2px gray;
  padding: 1rem;
  overflow-y: scroll;
  height: 320px;
  display: flex;
  flex-direction: column;
  gap: .5rem;

}

.message__author {
  color: gray;
}

.message__text {
  padding: .3rem;
  border-radius: 5px;
  display: inline-block;
}

@media (min-width: 768px) { 
  .chat {
    height: 370px;
  }
}

@media (min-width: 1280px) { 
  .chat {
    height: 450px;
  }
}


</style>