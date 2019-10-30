<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">手牌記録</router-link> |
      <router-link to="/about">記録閲覧</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

/*����style*/
.btn-border {
  display: inline-block;
  max-width: 180px;
  text-align: left;
  border: 2px solid #9ec34b;
  font-size: 16px;
  color: #9ec34b;
  text-decoration: none;
  font-weight: bold;
  padding: 8px 16px;
  border-radius: 4px;
  transition: .4s;
}

.btn-border:hover {
  background-color: #9ec34b;
  border-color: #cbe585;
  color: #FFF;
}
</style>
