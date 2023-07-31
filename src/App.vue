<template>
  
  <nav class="container-fluid">
    <div class="container-fluid">
      <div class="row">
        <div class="col-md-3">
          <router-link to="/" class="estiloHome"> <img src="./assets/logo.png" class="iconoGame webName">Online games</router-link>
        </div>
        <div class="col-md-6">
          <!-- DIV VACIO -->
        </div>
        <div class="col-md-3">
          <router-link to="/about" class="estiloAbout">About</router-link>
        </div>
      </div>
    </div>    
  </nav>
  <router-view/>
  
  <footer class="miFooter">
      
    <p>Copyright 2023  /  Marcelo Crisóstomo</p>
  </footer>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}



nav {
  padding: 30px;
 
  background-color: #16DB65;
  background-size: cover;
}

nav a {
  font-weight: bold;
  color: #fff;
  text-decoration: none;
}

.iconoGame{
  width: 64px;
  height: 64px;
  margin-right: 15px;
}

.miFooter{
  height: 50px;
  background-color: #16DB65 ;
  color: whitesmoke;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  padding-top: 15px;

}
</style>
