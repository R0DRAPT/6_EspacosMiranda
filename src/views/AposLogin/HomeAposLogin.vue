<template>
  <div>
    <Banner />
    <section class="main-container" style="background-color: #b49660; padding:20px; font-size: 18px; margin-right: 300px;">
      <h4 class="spacebetween" style="font-family: 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;">Bem Vindo <b>{{ username }}</b></h4>
      <p class="spacebetween paragrafo-main" style="font-family: verdana" >──────</p>
      <p class="spacebetween paragrafo-main"><b style="font-family: 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;">Agora já pode ver os nossos artigos</b></p>
      <p class="spacebetween paragrafo-main" style="font-family: 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;">Pode também comprar qualquer artigo que nós tenhamos.</p>
      <p class="spacebetween paragrafo-main" style="font-family: 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;">(Mudar Isto depois)</p>
    </section>
  
    <section style="color: white; display: flex; flex-wrap: wrap; justify-content: center; align-items: center; margin-top: 30px; ">
      <!-- Row 1 -->
      <div class="hover-box">1</div>
      <div class="hover-box">2</div>
      <div class="hover-box">3</div>
    </section>
    
    <section style="color: white; display: flex; flex-wrap: wrap; justify-content: center; align-items: center; margin-bottom: 30px;">
      <!-- Row 2 -->
      <div class="hover-box">4</div>
      <div class="hover-box">5</div>
      <div class="hover-box">6</div>
    </section>
  </div>
</template>

<script>
import Banner from "../../components/Banner.vue"

export default {
  name: "HomeAposLogin",

  mounted() {
    // Recupera Dados no localStorage
    const userData = JSON.parse(localStorage.getItem("Register-Info"));
    if (userData) {
      this.username = userData.username;

      toastr.success("Registado Com Sucesso", "Sucesso", {
        closeButton: true,
        positionClass: "toast-bottom-right",
        progressBar: true,
        timeOut: 5000,
        extendedTimeOut: 1000,
        preventDuplicates: true,
        showMethod: "fadeIn",
        hideMethod: "fadeOut",
        toastClass: "toast-success",
      });
    }
  },

  data() {
    return {
      username: "",
    };
  },

  components: {
    Banner,
    // ModalRegisterContent,
  }
}
</script>

<style scoped>
@import 'bootstrap/dist/css/bootstrap.min.css';

h4 {
  margin-left: 430px;
  text-align: left;
  font-size: 24px;
  color: #2b2a2a !important;
}

.paragrafo-main {
  margin-left: 430px;
  font-size: 20px;
}
.spacebetween {
  margin-bottom: -1px;
}

.hover-box {
  width: 340px;
  height: 300px;
  margin: 10px;
  background-color: #333;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.hover-box:hover {
    background-color: #555;
    cursor: pointer;
  }
</style>
