<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">手牌記録</router-link> |
      <router-link to="/about">記録閲覧</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style lang="scss">
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

/* common style */
$content-margin: 15px;
$content-padding: 10px;
$main-color: #9ec34b;

.horizontal-flex {
  display: flex;
  justify-content: center;
  margin-top: $content-margin;
  margin-bottom: $content-margin;
  padding: $content-padding;
  flex-wrap: wrap;
}
.btn-border {
  display: inline-block;
  max-width: 180px;
  text-align: left;
  border: 2px solid $main-color;
  font-size: 16px;
  color: $main-color;
  text-decoration: none;
  font-weight: bold;
  padding: 8px 16px;
  border-radius: 4px;
  transition: .4s;
}
.btn-border:hover {
  background-color: $main-color;
  border-color: #cbe585;
  color: #FFF;
}
</style>
