<template> 

    <div>
        <button :class="{active: isNum}" @click="isNum = !isNum">Numbered Notations</button>
        <button :class="{active: isHitbox}" >Hitboxes</button>
    </div>

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
            <button @click="this.$emit('update',command.moveImg)">{{ command.name }}</button>
        </div>
    </div>
    <div v-if="showSpecials" class="Specials">
        <div v-for="special in specials">
            <button  @click="this.$emit('update',special.moveImg)">
                <span v-if="isNum">{{ special.numName }}</span>
                <span v-else>{{ special.name }}</span>
            </button>
        </div>
    </div>
    <div v-if="showOverdrives" class="Overdrives">
        <div v-for="overdrive in overdrives">
            <button  @click="this.$emit('update',overdrive.moveImg)">
                <span v-if="isNum">{{ overdrive.numName }}</span>
                <span v-else>{{ overdrive.name }}</span>
            </button>
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
                isNum: false,
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