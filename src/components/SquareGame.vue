<template>
    <div 
        :class="['square', (size == 'big' ? 'big-square' : 'little-square')]"
        :style="size == 'big' ? ('background-color: ' + color) : null"
        @click="handleClick"
    >
        <p v-if="size == 'little'">{{ color }}</p>
    </div>
</template>

<script>
export default {
    props: {
        size: {
            type: String, 
            required: true
        }, 

        color: {
            type: String, 
            required: true
        }
    }, 

    methods: {
        handleClick() {
            this.$emit("clickOn")
        }
    }
}
</script>

<style>
.big-square {
    width: 540px;
    height: 300px;
}

.little-square {
    width: 170px;
    height: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    background-color: rgb(217, 216, 216);
}
</style>