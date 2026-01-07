<script setup>
const { width, height } = defineProps({
    width: {
        type: Number,
        default: 39,
    },
    height: {
        type: Number,
        default: 39,
    },
})
</script>

<template>
    <svg :width="width" :height="height" viewBox="0 0 39 39" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path fill-rule="evenodd" clip-rule="evenodd"
            d="M26.422 24.278L24.3 26.4L19.498 21.602L14.698 26.394L12.578 24.272L17.376 19.482L12.578 14.686L14.7 12.564L19.5 17.362L24.302 12.568L26.422 14.692L21.622 19.482L26.422 24.278ZM19.5 0C8.748 0 0 8.748 0 19.5C0 30.252 8.748 39 19.5 39C30.252 39 39 30.252 39 19.5C39 8.748 30.252 0 19.5 0Z"
            fill="#D00303" />
    </svg>
</template>

<style scope></style>