<script setup>
const props = defineProps({
    activeSlider: Number,
    direction: String,
    numberSliderElements: Number,
})

const emits = defineEmits(['clickOnSliderButton'])
</script>

<template>
    <button
        v-show="props.activeSlider !== 1 && props.direction === 'left'"
        @click="$emit('clickOnSliderButton')"
        class="slider-button slider-button--left"
    >
        <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="#fff"
            class="size-6"
        >
            <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 19.5 8.25 12l7.5-7.5" />
        </svg>
    </button>

    <button
        v-show="activeSlider !== props.numberSliderElements && props.direction === 'right'"
        @click="$emit('clickOnSliderButton')"
        class="slider-button slider-button--right"
    >
        <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="#fff"
            class="size-6"
        >
            <path stroke-linecap="round" stroke-linejoin="round" d="m8.25 4.5 7.5 7.5-7.5 7.5" />
        </svg>
    </button>
</template>

<style scoped></style>
