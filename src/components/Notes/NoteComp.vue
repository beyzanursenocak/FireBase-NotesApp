<template>
  <section>
    <base-card>
      <h1>My Note Application</h1>
      <form @submit.prevent="sendNotes">
        <div class="form-control">
          <label for="notes">Lütfen Notunuzu Giriniz :)</label>
          <input
            type="text"
            id="notes"
            name="notes"
            placeholder="Note"
            v-model.trim="enteredNotes"
          />
        </div>
        <div class="form-control">
          <h3>Lütfen Notunuzun Önem Derecesini Seçiniz :)</h3>
          <h4>
            1-(Önemsiz) 2-(Biraz Önemli) 3-(Orta Derece Önemli) 4-(Önemli)
            5-(Çok Önemli)
          </h4>
        </div>
        <div class="form-control">
          <input
            type="radio"
            id="onemlilikDerecesi-1"
            name="onemlilikDerecesi"
            value="1"
            v-model="onemli"
          />
          <label for="onemlilikDerecesi-1">1</label>

          <input
            type="radio"
            id="onemlilikDerecesi-2"
            name="onemli"
            value="2"
            v-model="onemli"
          />
          <label for="onemlilikDerecesi-2">2</label>

          <input
            type="radio"
            id="onemlilikDerecesi-3"
            name="onemli"
            value="3"
            v-model="onemli"
          />
          <label for="onemlilikDerecesi-3">3</label>

          <input
            type="radio"
            id="onemlilikDerecesi-4"
            name="onemli"
            value="4"
            v-model="onemli"
          />
          <label for="onemlilikDerecesi-4">4</label>

          <input
            type="radio"
            id="onemlilikDerecesi-5"
            name="onemli"
            value="5"
            v-model="onemli"
          />
          <label for="onemlilikDerecesi-5">5</label>
          <p v-if="bosBirakma">
            Not Kısmı veya Önem Derecesinden Biri Boş Olabilir Doldurduğunuzdan
            Emin Olunuz Lütfen, Teşekkürler :)
          </p>
          <p v-if="isError">{{ isError }}</p>
        </div>
        <base-button>Ekle</base-button>
      </form>
    </base-card>
  </section>
</template>

<script>
export default {
  data() {
    return {
      enteredNotes: "",
      onemli: null,
      bosBirakma: false,
      isError: null,
    };
  },
  methods: {
    sendNotes() {
      if (this.enteredNotes === "" || !this.onemli) {
        this.bosBirakma = true;
        return;
      }
      this.bosBirakma = false;

      console.log("Notes: " + this.enteredNotes);
      console.log("Önemi: ");
      console.log(this.onemli);
      
        this.isError = null;
      fetch("https://vue3-note-app-default-rtdb.firebaseio.com/notes.json", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          note: this.enteredNotes,
          onemlilikDerecesi: this.onemli,
        }),
      }).then((responce) => {
        if(responce.ok){
          //...
        }else {
          throw new Error('Not Yüklenemedi!');
        }
      }).catch((error) => {
        console.log(error);
        this.isError = error.message;

      })
      this.onemli = null;
      this.enteredNotes = "";
    },
  },
};
</script>

<style scoped>
.form-control {
  margin: 0.5rem 0;
}

input[type="text"] {
  display: block;
  width: 20rem;
  margin-top: 0.5rem;
  font-size: 15px;
}

input[type="radio"] {
  margin: 0 5px 0 100px;
}

h1 {
  color: rgb(25, 25, 112);
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  font-size: 40px;
}

h3 {
  color: rgb(25, 25, 112);
}

h4 {
  color: rgb(25, 25, 112);
  margin: 0 5px 0 100px;
}

p {
  color: rgb(25, 25, 112);
}

label {
  color: rgb(25, 25, 112);
}
</style>