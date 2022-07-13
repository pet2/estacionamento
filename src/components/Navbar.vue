<template>
  <div id="nav">
    <router-link to="/">
    </router-link>
    <router-link to="/">Pagina Principal</router-link> |
    
    <router-link to="/cadastro">Veiculos Cadastrados</router-link>
  </div>
</template>
<script>

    export default {
        name: "Navbar",
        props: ["logo", "alt"]  
    }

</script>

<style scoped>

  #nav {
    background-color: lightgray;
    padding: 15px 50px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
  }

  #nav #logo-url{
    margin: auto;
    margin-left: 0;;
  }

  #logo {
    width: 40px;
    height: 40px;
  }

  #nav a{

    color: blue;
    text-decoration: none;
    margin: 12px;
    transition: .5s;
    font-size: 20px;
   
  }
  
 #nav a:hover{
   color: rgb(72, 200, 72);

 }

</style>
