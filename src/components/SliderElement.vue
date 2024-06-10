<script setup>
const props = defineProps({
    slideDirectionRight: Boolean,
    activeSlider: Number,
    showWhenActiveSliderIs: Number,
})
</script>

<template>
    <Transition :name="props.slideDirectionRight ? 'slide-right' : 'slide-left'">
        <div
            v-show="props.showWhenActiveSliderIs === activeSlider"
            :aria-current="props.showWhenActiveSliderIs === activeSlider ? 'true' : 'false'"
            class="slider__slider-element"
        ></div>
    </Transition>
</template>

<style scoped></style>
