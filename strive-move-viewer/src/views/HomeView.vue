<template>
  <div class="home">
    <h1>Guilty Gear Strive Move Viewer</h1>
    <div class="characterSelect" v-if="characters.length">
      <div v-for="character in characters" :key="character.id">
        <RouterLink :to="{ name: 'character', params: {id: character.id}}">
         <img class="homeImg" :src=character.homeImg />
        </RouterLink>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'HomeView',
  data() {
    return {
      characters: []
    }
  },
  components: {},
  mounted() { 
    fetch('http://localhost:3000/characters')
    .then(res => res.json())
    .then(data => this.characters = data)
    .catch(err=> console.log(err.message))
  }
}
</script>

<style>

.characterSelect {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  height: 200px;
  max-width: 80vh;
  padding: 10px;
  margin: 10px auto;
}
img.homeImg
{
  display: block;
  cursor: pointer;
}
</style>
