<script setup>
import IconHeart from './Icons/IconHeart.vue';

const { count } = defineProps({ count: { type: Number, default: 0 } })
</script>

<template>
    <span class="score">
        <span class="score-count">
            {{ count }}
        </span>
        <span>
            <IconHeart />
        </span>
    </span>
</template>

<style scope>
.score {
    background-color: var(--color-secondary-3);
    padding: 12px 24px;
    gap: 10px;
    display: inline-flex;
    align-items: center;
    border-radius: 36px;
    justify-content: space-between;
}

.score-count {
    font-weight: 700;
    font-size: 16px;
    line-height: 24px;
    color: var(--color-secondary);
}
</style>