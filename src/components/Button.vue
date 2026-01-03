<script setup>

</script>

<template>
    <button class="button">
        <div>
            <slot name="icon"></slot>
        </div>
        <slot></slot>
    </button>
</template>

<style scope>
.button {
    border: none;
    border-radius: 10px;
    padding: 14px;
    background: var(--gradient);
    font-family: var(--font);
    font-size: 20px;
    font-weight: 600;
    color: var(--color-primary);
    cursor: pointer;
}

.button:hover {
    background: var(--gradient-inverted);
}
</style>