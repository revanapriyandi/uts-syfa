<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
      <img src="../assets/alquran.jpg" class="rounded-circle" alt="my poto" width="30" height="30">
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <Link class="nav-link active" aria-current="page" href="/">Home</Link>
          </li>
          <li class="nav-item">
            <Link class="nav-link active" aria-current="page" href="about">About Developer</Link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>
<script>
import {Link} from 'vue-router'
export default {
  name : 'Navbar',
  components: {
    Link
  }

}
</script>

<style>
a{
  font-family: "ui-monospace";
}

</style>