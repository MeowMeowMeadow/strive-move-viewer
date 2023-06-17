<template> 

    <div>
        <button :class="{active: isNum}" @click="isNum = !isNum">Numbered Notations</button>
        <button :class="{active: isHitbox}" @click="isHitbox = !isHitbox">Hitboxes</button>
    </div>

    <div class="MoveButtons">
        <button :class="{active: showNormals}" @click="toggleNormals">Normals</button>
        <button :class="{active: showCommand}" @click="toggleCommand">Command Normals</button>
        <button :class="{active: showSpecials}" @click="toggleSpecials">Specials</button>
        <button v-if="isSpells" :class="{active: showSpells}" @click="toggleSpells">Spells</button>
        <button :class="{active: showOverdrives}" @click="toggleOverdrives">Overdrives</button>
    </div>
    <div v-if="showNormals" class="Normals">
        <div v-for="normal in moves">
            <button v-if="isHitbox" @click="this.$emit('update',normal.hitboxImg)">{{ normal.name }}</button>
            <button v-else @click="this.$emit('update',normal.moveImg)">{{ normal.name }}</button>
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
    <div v-if="showSpells" class="Spells">
        <div v-for="spell in spells">
            <button @click="this.$emit('update',spell.moveImg)">{{ spell.name }}</button>
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
                showSpells: false,
                isNum: false,
                isHitbox: false
            }
        },
        methods:
        {
            toggleNormals() {
                this.showNormals = !this.showNormals
                this.showCommand = false
                this.showSpecials = false
                this.showOverdrives = false
                this.showSpells = false
            },
            toggleCommand() {
                this.showCommand = !this.showCommand
                this.showNormals = false
                this.showSpecials = false
                this.showOverdrives = false
                this.showSpells = false
            },
            toggleSpecials() {
                this.showSpecials = !this.showSpecials
                this.showNormals = false
                this.showOverdrives = false
                this.showCommand = false
                this.showSpells = false
            },
            toggleOverdrives() {
                this.showOverdrives = !this.showOverdrives
                this.showNormals = false
                this.showSpecials = false
                this.showCommand = false
                this.showSpells = false
            },
            toggleSpells() {
                this.showSpells = !this.showSpells
                this.showNormals = false
                this.showSpecials = false
                this.showCommand = false
                this.showOverdrives = false
            }
        },
        props: ['moves', 'commands', 'specials', 'overdrives', 'uri', 'spells', 'isSpells']
    }
</script>

<style>
.MoveButtons {
    display: flex;
    align-items: center;
    width: 30%;
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

.Spells {
    width: 95% !important;
    margin: 0 auto;
    display: flex;
    align-items: center;
    justify-items: flex-start;
    justify-content: center;
    gap: 1rem;
    flex-wrap: wrap;
}

.active {
    background-color: aqua;
}
</style>