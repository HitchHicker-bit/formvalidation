<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style lang="sass">
#app 
  font-family: Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50


#nav 
  padding: 30px

  a 
    font-weight: bold
    color: #2c3e50

    &.router-link-exact-active 
      color: #42b983

.error
  color: red
  font-size: 12px     
  font-family: 'Rubik', sans-serif;

.invalid
  border-bottom: 2px solid red

.valid
  border-bottom: 2px solid #8cff5e

input:focus
  outline: none
  
.personal
  border-top: none
  border-left: none
  border-right: none
  height: 25%
  width: 50%
  padding-top: 5px
  padding-bottom: 5px
  font-size: 15px
  font-family: 'Rubik', sans-serif


</style>
