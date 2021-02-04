<template>
  
  <div class="content" id="app">

      <nav class="navbar" role="navigation" aria-label="main navigation">
  <div class="navbar-brand">
    <a class="navbar-item" href="https://bulma.io">
      <img src="https://bulma.io/images/bulma-logo.png" width="112" height="28">
    </a>

    <a role="button" class="navbar-burger" aria-label="menu" aria-expanded="false" data-target="navbarBasicExample" @click="isOpen = !isOpen" v-bind:class="{'is-active': isOpen}">
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
    </a>
  </div>

  <div id="navbarBasicExample" class="navbar-menu" v-bind:class="{'is-active': isOpen}">
    <div class="navbar-start">
      <router-link to="/" class="navbar-item">Home</router-link>
      <router-link to="/news" class="navbar-item">News</router-link>
    </div>
    
  </div>
</nav>
    
<!--Rendering the componenets will be here-->
    <router-view/>
</div>
</template>
<script>
export default {
  name: 'App',
     data: function() {
       return {
           isOpen: false
       }
   }
}


</script>

<style >

</style>