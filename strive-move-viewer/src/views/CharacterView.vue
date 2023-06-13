<template>
<button @click="goBack">Return Home</button>
    <div v-if="img">
        <h1>{{ name }}</h1>
        <img class="portrait" :src=img />
    </div>
    <div v-else>
        <h1>Loading...</h1>
    </div>
    <Move
     :moves="moves" :commands="commands" :specials="specials" :overdrives="overdrives" :uri="uri"
     @update="handleUpdate"
     />
</template>

<script>
import Move from '../components/Move.vue'

    export default {
        data() {
            return {
                uri: 'http://localhost:3000/characters/' + this.id,
                name: '',
                img: '',
                moves: [],
                commands: [],
                specials: [],
                overdrives: []

            }
        },
        mounted()
        {
            fetch(this.uri)
            .then(res => res.json())
            .then(data => {
                this.name = data.name
                this.img = data.portraitImg
                this.moves = data.moves
                this.commands = data.commandMoves
                this.specials = data.specials
                this.overdrives = data.overdrives
            })
        },
        props: ['id'],
        methods:
        {
            goBack()
            {
                this.$router.push('/')
            },
            handleUpdate(move) {
                this.img = move
            }
            
        },
        components: {Move}
    }
</script>

<style>
.portrait {
    height: 500px;
    width: 400px;
}

button {
    padding: 10px;
    border: none;
    cursor: pointer;
    border-radius: 10px;
    display: block;
    margin: 10px auto;
    background-color: #59627c;
    font-weight: bold;
    font-size: 1rem;
    box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
}

button:hover {
    background-color: rgb(226, 226, 226);
}
</style>