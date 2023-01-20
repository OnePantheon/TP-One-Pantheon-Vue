<template>
    <section class="modal">
        <div class="modal-content">
            <slot></slot>
            <button @click="nextGame">Suivant</button>
        </div>
    </section>
</template>

<script>
export default {
    methods: {
        nextGame() {
            this.$emit("nextGame")
        }
    }
}
</script>

<style>
.modal {
    position: fixed;
    top: 0px;
    left: 0px;
    right: 0px;
    bottom: 0px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #1119;
}

.modal-content {
    background-color: white;
    width: 300px;
    height: 100px;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    gap: 15px;
}
</style>