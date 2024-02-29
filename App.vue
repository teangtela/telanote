<script setup>
import { ref } from "vue";
const showModal = ref(false);
const deleteModal = ref(true);
const newNote = ref("");
const notes = ref([]);
const errorMessage = ref("");

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}
const addNote = () => {
  if (newNote.value.length < 10) {
    return (errorMessage.value = "Note need more than 10 characters");
  } else {
    errorMessage.value = "";
  }

  notes.value.push({
    id: Math.floor(Math.random() * 10000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: getRandomColor(),
  });
  showModal.value = false;
  newNote.value = " ";
};
</script>
<template>
  <main>
    <div v-show="showModal" class="overlay">
      <div class="modal">
        <textarea
          v-model.trim="newNote"
          name="note"
          id="note"
          cols="30"
          rows="10"
        ></textarea>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <button @click="addNote">Add Notes</button>
        <button @click="showModal = false" class="closed">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div
          v-for="note in notes"
          :key="note.id"
          :style="{ backgroundColor: note.backgroundColor }"
          class="card"
        >
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString(en - US) }}</p>
          <!-- <button @click="deleteModal = false" id="delete">
            X
          </button> -->
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  height: 100vh;
  padding: 0;
  margin: 0;
  width: 100%;
  font-family: sans-serif;
}
.main-text {
  color: black;
  margin-top: 6px;
  width: 100%;
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
  font-size: 50px;
  color: black;
  font-family: sans-serif;
}
header button {
  padding: 6px;
  border: none;
  width: 40px;
  height: 40px;
  border-radius: 6px;
  color: white;
  font-size: 20px;
  background-color: black;
  cursor: pointer;
}
.card {
  margin-top: 30px;
  width: 200px;
  height: 200px;
  background-color: rgb(237, 182, 44);
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 10px;
  margin-bottom: 10px;
  position: relative;
}
#delete {
  position: absolute;
  width: 20px;
  height: 20px;
  display: flex;
  justify-content: center;
  font-size: 17px;
  align-items: center;
  cursor: pointer;
  top: -5px;
  left: 203px;
  z-index: 20;
  border: none;
  background-color: red;
  border-radius: 50%;
  color: white;
}
.date {
  font-size: 12.5px;
  font-weight: bold;
  color: rgb(0, 0, 0);
}
.cards-container {
  display: flex;
  flex-wrap: wrap;
}
.overlay {
  position: absolute;
  width: 100%;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.77);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}
.modal {
  width: 600px;
  background-color: white;
  border-radius: 5px;
  padding: 20px;
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
  border-radius: 3px;
}
.modal .closed {
  background-color: red;
  margin-top: 5px;
}
.modal p {
  color: red;
}
</style>
