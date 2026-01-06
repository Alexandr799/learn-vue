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
    border-radius: 100px;
    padding: 20px 110px;
    background-color: var(--color-secondary);
    font-family: var(--font);
    font-size: 24px;
    font-weight: 400;
    color: var(--color-primary);
    cursor: pointer;
    transition: background-color 0.3s ease-in-out;
}

.button:hover {
    background-color: var(--color-secondary-2);
    transition: background-color 0.3s ease-in-out;
}
</style>