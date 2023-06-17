<template>
<button @click="goBack">Return Home</button>
<div class="content">
    <div v-if="img">
        <h1>{{ name }}</h1>
        <img class="portrait" :src=img />
    </div>
    <div v-else>
        <h1>Loading...</h1>
    </div>
    <div class="moveInfo">
        <h3>Move Information</h3>
        <p>Start Up: {{ startUp }}</p>
        <p>Move Type: {{ moveType }}</p>
        <p>On Block: {{ onBlock }}</p>
    </div>
</div>
    
    <Move
     :moves="moves" :commands="commands" :specials="specials" :overdrives="overdrives" :uri="uri" :spells="spells" :isSpells="isSpells"
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
                overdrives: [],
                spells: [],
                moveEnabled: false,
                isSpells: false,
                startUp: "N/A",
                moveType: "N/A",
                onBlock: "N/A"

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
                if(data.isSpells)
                {
                    this.isSpells = data.isSpells
                    this.spells = data.spells
                }
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
                this.moveEnabled = true
            }
            
        },
        components: {Move}
    }
</script>

<style>
.content {
    display: block;
}

.moveInfo {
    position: absolute;
    padding: 20px;
    margin-bottom: 15px;
    width: 500px;
    height: 100px;
    top: 100px;
    right: 350px;
}

.portrait {
    height: 50%;
    width: 50%;
    max-width: 350px;
    max-height: 500px;
    padding: 20px;
    margin-bottom: 15px;
    border-radius: 20px;
    border: 1px solid black;
    box-shadow: 5px 7.5px rgba(0, 0, 0, 0.26);
    background-color: rgba(89, 98, 124, 0.411);
}

.plus {
    color: rgb(71, 252, 71);
}

.negative {
    color: rgb(255, 82, 82);
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