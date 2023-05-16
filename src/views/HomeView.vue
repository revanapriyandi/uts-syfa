<script setup>
import Navbar from "../components/Navbar.vue";

import { onMounted } from "vue";

onMounted(()=>{
  document.getElementsByTagName("body")[0].style.backgroundImage = "Url('src/assets/bghome.jpg')"
  document.getElementsByTagName("body")[0].style.backgroundSize = "cover";
})
</script>

<script>
import axios from "axios";

export default {
  data() {
    return {
      ayah: [],
      audio: null,
      namaSurah: null,
      inputnomor: "",
    };
  },

  methods: {
    async submit() {
      let nomor = this.inputnomor;
      let ayat = `https://api.quran.com/api/v4/quran/verses/uthmani?chapter_number=${nomor}`;
      let arti = "https://api.quran.com/api/v4/quran/translations/134?chapter_number=" + nomor;

      let judul = "https://api.quran.com/api/v4/chapters?language=en";
      let suara = "https://api.quran.com/api/v4/chapter_recitations/2?language=en";

      if (nomor <= 0 || nomor > 114) {
        alert("nomor surah yang dimasukkan salah!");
      } else {
        const reqJudul = axios.get(judul);
        const reqAyat = axios.get(ayat);
        const reqSuara = axios.get(suara);
        const reqArti = axios.get(arti);

        axios.all([reqAyat, reqArti, reqJudul, reqSuara]).then(
          axios.spread((...response) => {
            const responseAyat = response[0];
            const responseArti = response[1];
            const responseJudul = response[2];
            const responseSuara = response[3];

            const a = responseAyat.data.verses;
            const b = responseArti.data.translations;

            const gabung = (a, b) => {
              const res = [];

              for (let i = 0; i < a.length + b.length; i++) {
                if (i % 2 === 0) {
                  res.push(a[i / 2]);
                } else {
                  res.push(b[(i - 1) / 2]);
                }
              }
              return res;
            };

            this.ayah = gabung(a, b);
            this.audio = responseSuara.data.audio_files[nomor - 1];
            this.namaSurah = responseJudul.data.chapters[nomor - 1];
          })
        );
      }
    },
  },
};
</script>

<template>
  <main>
    <Navbar/>
    <div class="title">
      <h1 class="jdl">Qur'an Ku</h1>
    </div>
    <div class="ket">
      <p>Ini adalah web Qur'an Ku yang saya buat untuk membantu Anda mencari Surah Al Qur'an.<br>
        Silahkan tulis nomor surah yang Anda ingin cari di web ini</p>
    </div>

    <section class="search">
      <input type="number" v-model="inputnomor" class="input" placeholder="Masukkan urutan surah" />
      <button class="btn btn-primary" @click="submit" type="submit">Cari</button>
    </section>

    <section class="container my-5">
      <div class="row justify-content-center">
        <div class="col-12">
          <div class="card rounded shadow">
            <div class="card-header display-5 text-center fw-bolder">
              <p v-if="namaSurah" class="judul">{{ namaSurah.name_simple }}</p>
              <p v-if="namaSurah" class="judul fs-1">{{ namaSurah.name_arabic }}</p>
              <p v-if="namaSurah" class="judul fs-6 text-start fw-normal">Jumlah Ayat : {{ namaSurah.verses_count }}</p>
              <p v-if="namaSurah" class="judul fs-6 text-start fw-normal">Diturunkan di : {{ namaSurah.revelation_place }}</p>
              <p v-if="namaSurah" class="judul fs-6 text-start fw-normal">Surah ke : {{ namaSurah.revelation_order }} diturunkan</p>
              <p v-if="audio">
                <audio controls class="suara1">
                  <source :src="audio.audio_url" type="audio/mpeg" />
                  Browser Anda tidak mendukung elemen audio.
                </audio>
              </p>
            </div>
            <div class="bismillah"></div>
            <div class="ayat" v-for="ayat in ayah" :key="ayat.id">{{ ayat.text_uthmani }} {{ ayat.text }}</div>
          </div>
        </div>
      </div>
    </section>

  </main>

</template>

<style>
.jdl{
  font-family: "Century Schoolbook";
}
.title{
  text-align: center;
}
.ket{
  text-align: center;
}
.search {
  display: flex;
  margin: 50px 0 0 0;
  flex-direction: row;
  justify-content: center;
}
.ayat {
  color: #4c4c4c;
  list-style: none;
  margin: 0 100px 30px 100px;
}

.ayat:nth-child(odd) {
  text-align: right;
  font-size: 40px;
}
.ayat:nth-child(even) {
  text-align: left;
  font-size: 15px;
  color: #747474;
}

</style>