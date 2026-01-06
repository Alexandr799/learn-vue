<script setup>
const emit = defineEmits(['changeStatus', 'turn'])
const { word, number } = defineProps({
    word: {
        type: String,
        default: '',
    },
    number: {
        type: String,
        default: '01',
    }
})
</script>

<template>
    <article class="card">
        <div class="border">
            <span class="number">
                {{ number }}
            </span>
            {{ word }}
            <button class="changebutton">
                Перевернуть
            </button>
        </div>
    </article>
</template>

<style scope>
.card {
    height: 376px;
    border-radius: 16px;
    background-color: var(--color-card);
    padding: 25px 19px;
    box-shadow: 0px 0px 16px 0px #0000001A;
}

.number {
    position: absolute;
    top: -7px;
    left: 17px;
    z-index: 1;
    font-weight: 400;
    font-size: 14px;
    line-height: 100%;
}

.border {
    border-radius: 12px;
    border: 1px solid var(--color-secondary-3);
    height: 100%;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
}

.changebutton {
    position: absolute;
    left: 50%;
    bottom: -11px;
    transform: translateX(-50%);
    background-color: var(--color-card);
    border: none;
    cursor: pointer;
    text-transform: uppercase;
    font-size: 12px;
    font-weight: 700;
    line-height: 18px;
    letter-spacing: 12%;
}
</style>