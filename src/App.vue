<template>
  <main>
    <div class="overlay" v-if="showModal">
      <div class="modal">
        <div class="header mb-4">
          <h4>Create a New Note</h4>
        </div>
        <textarea
          v-model.trim="newNote"
          name="note"
          id="note"
          cols="30"
          rows="10"
        ></textarea>
        <p v-if="errorMessage" class="text-danger">{{ errorMessage }}</p>
        <div class="d-flex flex-row justify-content-end mt-4">
          <button class="btn btn-primary me-3" @click="this.addNote">
            Add Note
          </button>
          <button class="btn btn-danger" @click="showModal = false">
            Close
          </button>
        </div>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div class="container d-flex justify-content-start">
          <div
            v-for="note in notes"
            :key="note.id"
            class="card"
            :style="{ backgroundColor: note.backgroundColor }"
          >
            <p class="main-text">
              {{ note.text }}
            </p>
            <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "Notes",

  data() {
    return {
      errorMessage: "",
      newNote: "",
      notes: [],
      showModal: false,
    };
  },
  methods: {
    getRandomColor() {
      const color = "hsl(" + Math.random() * 360 + ", 100%, 75%)";
      return color;
    },
    addNote() {
      if (this.newNote.length < 10) {
        this.errorMessage = "Please enter a minimum of 10 characters!";
        return;
      }

      this.notes.push({
        id: Math.floor(Math.random() * 1000000),
        text: this.newNote,
        date: new Date(),
        backgroundColor: this.getRandomColor(),
      });
      this.showModal = false;
      this.newNote = "";
      this.noteError = "";
      this.errorMessage = "";
    },
  },
};
</script>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
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
}

header button {
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

.date {
  font-size: 12.5px;
  font-weight: bold;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.77);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  width: 750px;
  height: 300px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}

.main-text {
  color: black;
  font-weight: 600;
}

.date {
  color: black;
  font-weight: 600;
}
</style>
