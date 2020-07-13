<template>
  <div id="app">
    <div class="wrapper bgded overlay" style="background-image:url('https://external-preview.redd.it/jeL1W8MjDEefLiYRSdYHik6o9bXO83vMODH-xVY8ydI.jpg?auto=webp&s=fe1c69e516f73b2f4829b9d91c9db1df75403cfe');">

      <div class="wrapper">
        <div id="pageintro" class="hoc clear"> 
          <article>
            <h2 class="heading">Erik's Movie App</h2>
            <p>New and Improved!</p>
          </article>
        </div>
      </div>
      <div class="wrapper row1">
        <header id="header" class="hoc clear"> 
      
          <nav id="mainav" class="fl_right">
            <ul class="clear">
              <li ><router-link to="/">Home</router-link></li>
              <li ><router-link to="/movies">All Movies</router-link></li>
              <li ><router-link to="/movies/new">Add Movie</router-link></li>
              <li  v-if="!isLoggedIn()"><router-link to="/signup">Signup</router-link></li>
              <li  v-if="!isLoggedIn()"><router-link to="/login">Login</router-link></li>
              <li  v-if="isLoggedIn()"><router-link to="/logout">Logout</router-link></li>
            </ul>
          </nav>
        </header>
      </div>
    </div>

    
    <router-view />
    

    <div class="wrapper row4">
      <footer id="footer" class="hoc clear"> 
        
        <div class="one_quarter first">
          <h6 class="title">Contact</h6>
          <address class="btmspace-30">
          123 ABC Street <br>
          DEFburg, TN<br>
          54321
          </address>
          <ul class="nospace">
            <li class="btmspace-10"><i class="fa fa-phone"></i>917-867-5309</li>
            <li><i class="fa fa-envelope-o"></i> movies@domain.com</li>
          </ul>
        </div>
        <div class="one_quarter">
          <h6 class="title">About Us</h6>
          <article>
            <h2 class="nospace font-x1"><a href="#">Dictum dui quisque</a></h2>
            <time class="font-xs" datetime="2045-04-06">Friday, 6<sup>th</sup> April 2045</time>
            <p>Lacinia gravida accumsan proin tincidunt auctor pharetra mauris id luctus tellus morbi eu magna sit amet.</p>
          </article>
        </div>
        <div class="one_quarter">
          <h6 class="title">Terms of Service</h6>
          <ul class="nospace linklist">
            <li><a href="#">Lobortis cursus sodales</a></li>
            <li><a href="#">Libero at iaculis sem morbi</a></li>
            <li><a href="#">Sed augue in sapien facilisis</a></li>
            <li><a href="#">Sollicitudin ut nec felis</a></li>
            <li><a href="#">Praesent maximus quam</a></li>
          </ul>
        </div>
        <div class="one_quarter">
          <h6 class="title">More Info</h6>
          <p>Sit amet egestas porttitor metus ante ornare ipsum iaculis dapibus ante est.</p>
          <p>Convallis elit sagittis dapibus interdum proin a diam vel quam suscipit pharetra.</p>
        </div>
       
      </footer>
    </div>

  </div>
</template>



<style>
.container {
  margin: auto;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
  padding: 10px;
}
</style>

<script>
export default {
  data: function() {
    return {};
  },
  methods: {
    isLoggedIn: function() {
      return localStorage.getItem("jwt");
    }
  }
};
</script>