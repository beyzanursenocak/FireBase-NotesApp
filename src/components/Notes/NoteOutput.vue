<template>
  <section>
    <base-card>
      <h1>Notes</h1>
      <div>
        <base-button @click="loadNotes">Notları Görüntüle</base-button>
      </div>
      <p v-if="isLoading">Loading...</p>
      <p v-else-if="!isLoading && isError">{{ isError }}</p>
      <p v-else-if="!isLoading && (!results || results.length === 0)">Girilen bir notunuz yok. Notlarınızı listelemek için ilk olarak not giriniz lütfen.</p>
      <ul v-else>
        <note-result
          v-for="result in results"
          :key="result.id"
          :note="result.note"
          :onemlilikDerecesi="result.onemlilikDerecesi"
        >
        </note-result>
      </ul>
    </base-card>
  </section>
</template>

<script>
import NoteResult from "./NoteResult.vue";
export default {
  components: {
    NoteResult,
  },
  data() {
    return {
      results: [],
      isLoading: false,
      isError: null,
    };
  },
  methods: {
    loadNotes() {
      this.isLoading = true;
      fetch("https://vue3-note-app-default-rtdb.firebaseio.com/notes.json")
        .then((responce) => {
          if (responce.ok) {
            return responce.json();
          }
        })
        .then((data) => {
          this.isLoading = false;
          const results = [];
          for (const id in data) {
            results.push({
              id: id,
              note: data[id].note,
              onemlilikDerecesi: data[id].onemlilikDerecesi,
            });
          }
          this.results = results;
        })
        .catch((error) => {
          console.log(error);
          this.isError = 'Sunucudan Kaynaklı Bir Hata Var. Lütfen Daha Sonra Tekrar Deneyiniz.';
          this.isLoading = false;
        })
    },
  },
  mounted() {
    this.loadNotes();
  },
};
</script>

<style scoped>
.form-control {
  margin: 0.5rem 0;
}

h1 {
  color: rgb(25, 25, 112);
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  font-size: 40px;
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>