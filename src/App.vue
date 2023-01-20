<template>
    <div>
        <main class="game">
            <SquareGame 
                :color="answer"
                size="big"
            />

            <section>
                <SquareGame
                    v-for="choice in arrayChoice"
                    :key="choice"
                    :color="choice"
                    size="little"
                    @clickOn="handleClick(choice)"
                />
            </section>
        </main>

        <ResModal 
            v-if="showRes"
            @nextGame="nextGame"
        >
            <p v-if="res">Vous avez validé le défi</p>
            <p v-else>Vous avez échoué le défi</p>
        </ResModal>
    </div>
</template>

<script>
import SquareGame from './components/SquareGame.vue';
import { ref } from 'vue';
import ResModal from './components/ResModal.vue';

export default {
    name: 'App',
    components: {
    SquareGame,
    ResModal
}, 

    setup() {
        const answer = ref(""), arrayChoice = ref([]), res = ref(false), showRes = ref(false);
        
        return { answer, arrayChoice, res, showRes }
    },  

    created() {
        this.generateColor();
    },

    methods: {
        randomColor() {
            const maxValue = 0xFFFFFF;
            const randomValue = Math.floor(Math.random() * maxValue)
                .toString(16)
                .toUpperCase()
                .padStart(6, "0"); 
            
            return '#' + randomValue;
        },  

        shuffleArray() {
            const index = Math.floor(Math.random() * 3);
            const temp = this.arrayChoice[0];
            this.arrayChoice[0] = this.arrayChoice[index];
            this.arrayChoice[index] = temp;
        },  

        handleClick(choice) {
            this.res = choice == this.answer;
            this.showRes = true;
        }, 
        
        nextGame() {
            this.generateColor();
            this.showRes = false;
        },  

        generateColor() {
            this.arrayChoice = []
            this.answer = this.randomColor();
            this.arrayChoice[0] = this.answer;

            for(let i = 0; i < 2; i++) {
                let color = this.randomColor();
                while(this.arrayChoice.includes(color)) {
                    color = this.generateColor();
                }

                this.arrayChoice.push(color);
            }

            this.shuffleArray();
        }
    }
}
</script>

<style>
*, *::before, *::after {
    padding: 0px;
    margin: 0px;
    box-sizing: border-box;
}

.game {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

section {
    padding-top: 50px;
    display: flex;
    gap: 15px;
}
</style>