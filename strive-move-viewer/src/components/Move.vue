<template>
    <div class="MoveButtons">
        <button :class="{active: showNormals}" @click="toggleNormals">Normals</button>
        <button :class="{active: showCommand}" @click="toggleCommand">Command Normals</button>
        <button :class="{active: showSpecials}" @click="toggleSpecials">Specials</button>
        <button :class="{active: showOverdrives}" @click="toggleOverdrives">Overdrives</button>
    </div>
    <div v-if="showNormals" class="Normals">
        <div v-for="normal in moves">
            <button>{{ normal.name }}</button>
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
                showOverdrives: false
            }
        },
        methods:
        {
            toggleNormals() {
                this.showNormals = !this.showNormals
            },
            toggleCommand() {
                this.showCommand = !this.showCommand
            },
            toggleSpecials() {
                this.showSpecials = !this.showSpecials
            },
            toggleOverdrives() {
                this.showOverdrives = !this.showOverdrives
            }
        },
        props: ['moves', 'commands', 'specials', 'overdrives']
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
    justify-items: center;
    margin: 0 auto;
    gap: 1rem;
    width: 30%;
    flex-wrap: wrap;
}

.active {
    background-color: aqua;
}
</style>