<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style lang="scss">


//Fonts
@import url('https://fonts.googleapis.com/css2?family=Lato:wght@100;300;400;700&display=swap');
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
  ::-webkit-scrollbar {
    width: 5px;
  }
  ::-webkit-scrollbar-track {
    background-color: transparent;
  }
  ::-webkit-scrollbar-thumb {
    background-color: #d64933;
    border-radius: 25px;
  }
#app {
  font-family: 'Lato', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  a{
  text-decoration: none;
  color: initial;
  &:hover{
    text-decoration: none;
    color: initial;
  }

}
}
.button{
  background: #d64933;
  color: #fff;
  padding: 20px;
  border: none;
  transition: all 0.3s;
  border: 2px solid #d64933;
  border-radius: 8px;
  &:hover{
      background: none;
      color: #d64933;
  }
}
#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
