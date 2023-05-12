<script setup>
import { ref } from 'vue';

const showModal = ref(false)
const newNote = ref("")
const errorMessage = ref("")
const notes = ref([]);

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75% )";
  
}

const addNote = () => {
  if(newNote.value.length < 10){
    return errorMessage.value = "Notes need to be 10 characters"
  }
  notes.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: getRandomColor()
  });
  showModal.value = false;
  newNote.value=""
}


</script>
<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <button @click="addNote">Add note</button>
        <button class="close" @click="showModal = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
      <h1>Notes</h1>
      <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes"  :key="note.id" class="card" :style="{backgroundColor: notes.backgroundColor}">
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>
<style scoped>
main{
  width: 100vw;
  height: 100vh;
}
.container{
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}
header{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
h1{
  font-weight: bold;
  font-size: 75px;
  margin-bottom: 10px;
}
header button{
  border: none;
  border-radius: 100%;
  height: 50px;
  width: 50px;
  padding: 10px;
  background-color: aquamarine;
  cursor: pointer;
  color: aliceblue;
  font-size: 20px;
}
.card{
  height: 225px;
  width: 225px;
  padding: 10px;
  background-color: rgb(237, 182, 44);
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}
.date{
  font-size: 12.5px;
  color: black;
  font-weight: bold;
}
.cards-container{
  display: flex;
  flex-wrap: wrap;
}
.overlay{
  position: absolute;
  width: 100%;
  height: 100%;
  background-color:rgba(0,0,0,0.77);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal{
  width: 750px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}
.modal button{
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px;
}
.modal .close{
  background-color: brown;
  margin-top: 7px;
}
.modal p{
  color: red;
}
</style>