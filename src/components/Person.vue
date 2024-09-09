<script setup>
import { ref, onMounted, onBeforeMount } from 'vue'
import Loader from "./Loader.vue"
import axios from 'axios'

const emit = defineEmits(['customChange'])

const props = defineProps({
    alineacion: String
})

const person = ref({})
const loading = ref(false)
const mensaje = ref("")

const onSubmit = () => {
    if (!mensaje.value.trim()) {
        alert("Debe escribir un mensaje")
        return
    }

    emit('saveMessage', {
        title: person.value.title,
        alineacion: props.alineacion,
        texto: mensaje.value.trim()
    })

    mensaje.value = ""
}

onMounted(() => {
    loading.value = true;
    const getPerson = async () => {
        try {
            const { data } = await axios("https://randomuser.me/api/")
            const { name, picture, login } = data.results[0]
            person.value = {
                nombre: `${name.first} ${name.last}`,
                img: picture.large,
                title: login.username
            }
        } catch (err) {
            console.log(err.message)
        }
        loading.value = false;
    }

    getPerson()
})

</script>

<template>
    <form @submit.prevent="onSubmit" v-if="!loading" class="person">
        <div class="person__image">
            <img :src="person.img" alt="image">
        </div>
        <p :style="{
            textAlign: alineacion === 'izquierda' ? 'start' : 'end',
        }" class="person__name">{{ person.nombre }}</p>

        <div 
        class="person__bar"
        >
        <div 
        class="person__innerbar"
        :style="{
            backgroundColor: alineacion === 'izquierda' && 'rgb(193, 255, 234)'
        }"
        >

        </div>
    </div>

        <textarea @blur="focus = false" @focus="focus = true" v-model="mensaje" name="mensaje" id="mensaje"
            rows="5"></textarea>

        <button type="submit">enviar</button>
    </form>
    <div v-else>
        <Loader />
    </div>
</template>


<style scoped>
.person {
    display: flex;
    flex-direction: column;
    text-align: start;
    gap: .5rem;
}

.person__image img {
    object-fit: contain;
    width: 100%;
}

.person__bar {
    border: 1px solid gray;
    padding: .3rem;
    border-radius: 3px;
}

.person__innerbar {
    border: 1px solid gray;
    padding: .5rem;
    border-radius: 3px;
}

</style>