<script setup>
import { ref } from 'vue'
import SliderElement from './SliderElement.vue'
import SliderButton from './SliderButton.vue'
import SliderSelectItem from './SliderSelectItem.vue'

const props = defineProps({
    numberSliderElements: {
        type: Number,
        default: 1,
    },
})

const activeSlider = ref(1)
const slideDirectionRight = ref(true)

const toPreviousSlider = () => {
    if (activeSlider.value === 1) {
        slideDirectionRight.value = true
        activeSlider.value = props.numberSliderElements
    } else {
        activeSlider.value--
        slideDirectionRight.value = false
    }
}

const toNextSlider = () => {
    if (activeSlider.value < props.numberSliderElements) {
        activeSlider.value++
        slideDirectionRight.value = true
    } else {
        activeSlider.value = 1
        slideDirectionRight.value = false
    }
}

const updateActiveSlider = async (index) => {
    const distanceToNextSlider = Math.abs(index - activeSlider.value)
    let firstIteration = true
    if (index >= activeSlider.value) {
        slideDirectionRight.value = true
        for (let i = activeSlider.value; i <= index; i++) {
            activeSlider.value = i
            if (firstIteration) {
                firstIteration = false
                continue
            }
            if (distanceToNextSlider > 1) await new Promise((resolve) => setTimeout(resolve, 600))
        }
    } else {
        slideDirectionRight.value = false
        for (let i = activeSlider.value; i >= index; i--) {
            activeSlider.value = i
            if (firstIteration) {
                firstIteration = false
                continue
            }
            if (distanceToNextSlider > 1) await new Promise((resolve) => setTimeout(resolve, 600))
        }
    }
}

const selectItemIsActive = (index) => index + 1 === activeSlider.value
</script>

<template>
    <div class="slider">
        <SliderElement
            :activeSlider="activeSlider"
            :slideDirectionRight="slideDirectionRight"
            :showWhenActiveSliderIs="1"
            style="background-image: url('images/image-1.png')"
        />

        <SliderElement
            :activeSlider="activeSlider"
            :slideDirectionRight="slideDirectionRight"
            :showWhenActiveSliderIs="2"
            style="background-image: url('images/image-2.png')"
        />

        <SliderElement
            :activeSlider="activeSlider"
            :slideDirectionRight="slideDirectionRight"
            :showWhenActiveSliderIs="3"
            style="background-image: url('images/image-3.png')"
        />

        <SliderElement
            :activeSlider="activeSlider"
            :slideDirectionRight="slideDirectionRight"
            :showWhenActiveSliderIs="4"
            style="background-image: url('images/image-4.png')"
        />

        <div class="slider__buttons">
            <SliderButton
                @clickOnSliderButton="toPreviousSlider"
                direction="left"
                :activeSlider="activeSlider"
                :numberSliderElements="numberSliderElements"
            />
            <SliderButton
                @clickOnSliderButton="toNextSlider"
                direction="right"
                :activeSlider="activeSlider"
                :numberSliderElements="numberSliderElements"
            />
        </div>

        <div class="slider__select-items">
            <SliderSelectItem
                v-for="(_, index) in numberSliderElements"
                :key="index"
                :selectItemIsActive="selectItemIsActive(index)"
                @clickOnSliderSelectItem="updateActiveSlider(index + 1)"
            />
        </div>
    </div>
</template>

<style scoped>
.slide-left-enter-active {
    transition: all 0.6s ease-out;
}

.slide-left-leave-active {
    transition: all 0.6s ease-out;
}

.slide-left-enter-from {
    transform: translateX(-98%);
}

.slide-left-leave-to {
    transform: translateX(100%);
}

.slide-right-enter-active {
    transition: all 0.6s ease-out;
}

.slide-right-leave-active {
    transition: all 0.6s ease-out;
}

.slide-right-enter-from {
    transform: translateX(98%);
}

.slide-right-leave-to {
    transform: translateX(-100%);
}
</style>
