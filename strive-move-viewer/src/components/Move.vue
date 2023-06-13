<template>
    <div class="MoveButtons">
        <button :class="{active: showNormals}" @click="toggleNormals">Normals</button>
        <button :class="{active: showCommand}" @click="toggleCommand">Command Normals</button>
        <button :class="{active: showSpecials}" @click="toggleSpecials">Specials</button>
        <button :class="{active: showOverdrives}" @click="toggleOverdrives">Overdrives</button>
    </div>
    <div v-if="showNormals" class="Normals">
        <div v-for="normal in moves" :key="normal.name">
            <button @click="this.$emit('update',normal.moveImg)">{{ normal.name }}</button>
        </div>
    </div>
    <div v-if="showCommand" class="CommandNormals">
        <div v-for="command in commands">
            <button>{{ command.name }}</button>
        </div>
    </div>
    <div v-if="showSpecials" class="Specials">
        <div v-for="special in specials">
            <button>{{ special.name }}</button>
        </div>
    </div>
    <div v-if="showOverdrives" class="Overdrives">
        <div v-for="overdrive in overdrives">
            <button>{{ overdrive.name }}</button>
        </div>
    </div>
</template>

<script>
    export default {
        data()
        {
            return {
                showNormals: false,
                showCommand: false,
                showSpecials: false,
                showOverdrives: false,
                image: ''
            }
        },
        methods:
        {
            toggleNormals() {
                this.showNormals = !this.showNormals
                this.showCommand = false
                this.showSpecials = false
                this.showOverdrives = false
            },
            toggleCommand() {
                this.showCommand = !this.showCommand
                this.showNormals = false
                this.showSpecials = false
                this.showOverdrives = false
            },
            toggleSpecials() {
                this.showSpecials = !this.showSpecials
                this.showNormals = false
                this.showOverdrives = false
                this.showCommand = false
            },
            toggleOverdrives() {
                this.showOverdrives = !this.showOverdrives
                this.showNormals = false
                this.showSpecials = false
                this.showCommand = false
            }
        },
        props: ['moves', 'commands', 'specials', 'overdrives', 'uri']
    }
</script>

<style>
.MoveButtons {
    display: flex;
    align-items: center;
    width: 25%;
    margin: 0 auto;
}
.Normals, .CommandNormals, .Specials, .Overdrives {
    display: flex;
    align-items: center;
    justify-items: flex-start;
    justify-content: center;
    margin: 0 auto;
    gap: 1rem;
    width: 50%;
    flex-wrap: wrap;
}

.active {
    background-color: aqua;
}
</style>