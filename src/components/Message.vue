<script setup>

defineProps({
    mensaje: Object,
})

</script>

<template>
    <div :style="{
        textAlign: mensaje.alineacion === 'izquierda' ? 'start' : 'end'
    }" class="message">
        <h5 class="message__author">
            {{ mensaje.title }}
        </h5>
        <p :style="{
            backgroundColor: mensaje.alineacion === 'izquierda' ? 'rgb(193, 255, 234)' : '#FFF'
        }" class="message__text">
            <slot></slot>
        </p>
    </div>
</template>

<style scoped>
.message__author {
    color: gray;
    margin-bottom: .3rem;
}
.message__text {
    padding: .3rem;
    border-radius: 5px;
    display: inline-block;
    word-break: break-word;
}
</style>