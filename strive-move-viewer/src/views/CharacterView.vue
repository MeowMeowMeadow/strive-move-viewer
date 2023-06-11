<template>
<button @click="goBack">Return Home</button>
    <div v-if="img">
        <h1>{{ name }}</h1>
        <img class="portrait" :src=img />
    </div>
    <Move />
</template>

<script>
import Move from '../components/Move.vue'

    export default {
        data() {
            return {
                uri: 'http://localhost:3000/characters/' + this.id,
                name: '',
                img: ''

            }
        },
        mounted()
        {
            fetch(this.uri)
            .then(res => res.json())
            .then(data => {
                this.name = data.name
                this.img = data.portraitImg

            })
        },
        props: ['id'],
        methods:
        {
            goBack()
            {
                this.$router.push('/')
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
    background-color: rgb(196, 196, 196);
    font-weight: bold;
    font-size: 1rem;
}

button:hover {
    background-color: rgb(238, 89, 89);
}
</style>