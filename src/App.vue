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
  color: #41b879;
}

/*共通style*/
.btn-border {
  display: inline-block;
  max-width: 180px;
  text-align: left;
  border: 2px solid #41b879;
  font-size: 16px;
  color: #41b879;
  text-decoration: none;
  font-weight: bold;
  padding: 8px 16px;
  border-radius: 4px;
  transition: .4s;
  background-color: white;
}
label {
  display: inline-block;
  color: #41b879;
  font-weight: bold;
  font-size: 16px;
}
select {
  display: block;
  color: #41b879;
  border-color: #41b879;
  border-width: 2px;
  font-weight: bold;
  font-size: 16px;
  border-radius: 4px;
  padding: 4px;
  text-align: center;
}
input[type="number"] {
  display: inline-block;
  color: #41b879;
  border: 2px solid #41b879;
  font-size: 16px;
}
</style>
