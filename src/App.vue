<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <p v-if="newNote.length < 4 & newNote.length > 0"
          errorMessage>{{ errorMessage }}
          </p>
        <button v-if="newNote.length >= 4" @click="addNote"> Add note  </button>
        <button class="close" @click="showModal = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
    </div>
    <div class="cards-container">
      <div 
        v-for="note in notes" 
        :key="note.id"
        class="card" 
        :style="{backgroundColor: note.backgroundColor}"
      >
        <p class="main-text"> {{ note.text }} </p>
        <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";

const showModal = ref(false);
const newNote = ref("");
const notes = ref([]);
const errorMessage = 'Note needs to be minimum 4 chracter or more';
// Generate Random light color
function getRandomcolor(){
  return "hsl("+ Math.random() * 36000000 + ", 100%, 75%)";
}


const addNote = () => {
  notes.value.push({
    id: Math.floor(Math.random() * 10000000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: getRandomcolor()
  })
  showModal.value = false
  newNote.value = "";
}
</script>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
  background: white;
}

.container {
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
  color: black
}

Header  button {
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgb(21, 20, 20);
  border-radius: 100%;
  color: white;
  font-size: 20px;
}

.card {
    width: 225px;
    height: 225px;
    background-color: rgb(237, 182, 44);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
  }
  .cards-container {
    display: flex;
    flex-wrap: wrap;
    padding-left: 460px;
  }

  .main-text{
    color: black;
  }
  
  .date {
    color: black;
    font-size: 12.5px;
    font-weight: bold;
  }

  .overlay {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgb(0,0,0,0.77);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .modal {
    width: 750px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }
  .modal button {
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: blueviolet;
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;
  }
  .modal .close {
    background-color: red;
    margin-top: 7px;
  }

  .modal p {
    color: red;
  }
</style>