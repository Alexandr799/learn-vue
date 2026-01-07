<script setup>
import IconSuccess from './Icons/IconSuccess.vue';
import IconReset from './Icons/IconReset.vue';
import { computed } from 'vue';

const emit = defineEmits(['changeStatus', 'turn'])

const { word, number, translation, status, state } = defineProps({
    word: {
        type: String,
        default: '',
    },
    number: {
        type: Number,
        default: 0,
    },
    translation: {
        type: String,
        default: '',
    },
    status: {
        type: String,
        default: 'pending',
    },
    state: {
        type: String,
        default: 'closed',
    }
})

const numberPrepare = computed(()=>{
    const res = number + 1
    if (res < 10) {
        return '0' + res.toString()
    }
    return res.toString()
})

function turn() {
    emit('turn', 'opened', number)
}

function changeStatus(newStatus) {
    emit('changeStatus', newStatus, number)
}

</script>

<template>
    <article class="card">
        <div class="border">
            <span class="number">
                {{ numberPrepare }}
            </span>
            <span class="status-panel">
                <IconSuccess v-if="status === 'success'" />
                <IconReset v-if="status === 'fail'" />
            </span>
            {{ state === 'closed' && status === 'pending' ? word : translation }}
            <div v-if="state === 'opened'" class="choiseStatusPanel">
                <IconReset style="cursor: pointer;" :width="19.5" :height="19.5" @click="changeStatus('fail')" />
                <IconSuccess style="cursor: pointer;" :width="19.5" :height="19.5" @click="changeStatus('success')" />
            </div>
            <button v-if="state == 'closed' && status === 'pending'" class="turnbutton" @click="turn">
                Перевернуть
            </button>
            <span v-if="state === 'closed' && status !== 'pending'" class="endlabel">
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

.turnbutton,
.endlabel {
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