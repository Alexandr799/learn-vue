<script setup>
import { ref } from 'vue';
import SuccessIcon from './Icons/SuccessIcon.vue';
import IconReset from './Icons/IconReset.vue';

const emit = defineEmits(['changeStatus', 'turn'])

const { word, number, translate } = defineProps({
    word: {
        type: String,
        default: '',
    },
    number: {
        type: String,
        default: '01',
    },
    translate: {
        type: String,
        default: '',
    }
})

const status = ref('choising')
const isTurned = ref(false)


function turn() {
    isTurned.value = !isTurned.value
    emit('turn')
}

function changeStatus(newStatus) {
    isTurned.value = false
    status.value = newStatus
    emit('changeStatus')
}

</script>

<template>
    <article class="card">
        <div class="border">
            <span class="number">
                {{ number }}
            </span>
            <span v-if="status === 'success' || status === 'fail'" class="status-panel">
                <SuccessIcon v-if="status === 'success'"/>
                <IconReset v-if="status === 'fail'"/>
            </span>
            {{ !isTurned && status === 'choising' ? word : translate }}
            <button v-if="!isTurned && status === 'choising'" class="turnbutton" @click="turn">
                Перевернуть
            </button>
            <div v-if="isTurned" class="choiseStatusPanel">
                <IconReset style="cursor: pointer;" :width="19.5" :height="19.5" @click="changeStatus('fail')" />
                <SuccessIcon style="cursor: pointer;" :width="19.5" :height="19.5" @click="changeStatus('success')" />
            </div>
            <span v-if="!isTurned && status !== 'choising'" class="endlabel">
                ЗАВЕРШЕНО
            </span>
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

.turnbutton, .endlabel {
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

.choiseStatusPanel {
    display: flex;
    gap: 25px;
    padding: 3px 10px;
    position: absolute;
    align-items: center;
    justify-content: center;
    background-color: var(--color-card);
    bottom: -13px;
    left: 50%;
    transform: translateX(-50%);
}

.status-panel {
    position: absolute;
    top: -19px;
    left: 50%;
    transform: translateX(-50%);
}
</style>