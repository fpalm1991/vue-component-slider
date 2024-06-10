<script setup>
const props = defineProps({
    selectItemIsActive: Boolean,
    index: Number,
})

const emits = defineEmits(['clickOnSliderSelectItem'])
</script>

<template>
    <div
        class="select-item"
        :key="props.index"
        :class="props.selectItemIsActive ? 'active' : ''"
        @click="$emit('clickOnSliderSelectItem'), props.index"
    >
        <span class="select-item__visual">&nbsp;</span>
    </div>
</template>

<style scoped></style>
