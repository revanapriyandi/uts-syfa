<template>
  <Navbar/>
  <body>
  <div class="bodi">
    <div class="kanvas">
      <img src="../assets/syifa111..jpeg" class="rounded-circle img-thumbnail" alt="my poto" width="125" height="125" style="display: block; margin: auto">
      <h2 class="n1">Syifa Salsabilla</h2>
      <h5 class="h5">12050120344</h5>
      <hr>

      <p id="p1" class="p1">
        Saya adalah mahasiswa
        <br/>di Universitas Islam Negri Sultan Syarif Kasim Riau. Jurusan Teknik Informatika<br> Ini adalah web saya yang saya buat pada saat semester 6 sebagai tugas UTS<br>Matakuliah Pemrogramman Web
      </p>
      <br><br><br><br><br><br><br><br><br><br><br>
      <hr>
    </div>
  </div>
  </body>
  <footer>
    <p class="foot">Copyright &copy; 2023 Syifa Salsabilla.</p>
  </footer>

</template>
<script>
import Navbar from "../components/Navbar.vue";
export default {
  components: {Navbar}
}
</script>

<style>
.h5{
  text-align: center;
}
.n1{
  text-align: center;
}
.p1{
  text-align: center;
}
.kanvas{
  background: linear-gradient(white, lightseagreen);
  border-radius: 10px;
  width: 60%;
  margin-left: auto;
  margin-right: auto;

}
.bodi{
  background-image: url("../assets/bghome.jpg");
  padding: 30px;
}

</style>