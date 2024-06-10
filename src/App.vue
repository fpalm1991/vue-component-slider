<script setup>
import Slider from './components/Slider.vue'

const numberSliderElements = 4
</script>

<template>
    <header>
        <Slider :numberSliderElements="numberSliderElements" />
    </header>

    <main></main>

    <footer></footer>
</template>

<style scoped></style>
