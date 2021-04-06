<template>
  <div id="app">
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <header>
      <h1>Buttons Gallery</h1>
      <p>Choose your button or create one yourself</p>
    </header>
    <main>
      <Button title="Custom button" class="custom" :customizable="true"/>
      <Button title="<Button />" class="first"/>
      <Button title="<Button variant='outline'/>" class="second"/>
      <Button title="<Button variant='text'/>" class="third"/>
      <Button title="<Button disableShadow/>" class="fourth"/>
      <Button title="<Button disabled/>" :mustDisable="true" class="fifth"/>
      <Button title="<Button variant='text' disabled/>" :mustDisable="true" class="sixth"/>
      <Button title="<Button startIcon='help'/>" :mustLeftIcon="true" class="seventh"/>
      <Button title="<Button endIcon='help'/>"  :mustRightIcon="true" class="eighth"/>
      <Button title="<Button size='sm' />" :size="'sm'" class="ninth"/>
      <Button title="<Button size='md'/>" class="tenth"/>
      <Button title="<Button size='lg'/>" :size="'lg'" class="eleventh"/>
      <Button title="<Button color='default' />" class="twelfth first"/>
      <Button title="<Button color='primary' />" :color="'Primary'" class="thirteenth"/>
      <Button title="<Button color='secondary' />" :color="'Secondary'" class="fourteenth"/>
      <Button title="<Button color='danger'/>" :color="'Danger'" class="fifteenth"/>
    </main>
    <footer>
      Author: Marko Ilic
    </footer>
  </div>
</template>

<script>
import Button from './components/button'

export default {
  name: 'App',
  components: {
    Button
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  box-sizing: border-box;
  overflow: hidden;
  background: radial-gradient( #dce35b,#45b649);
}

h1 {font-size: 50px;}

.custom {text-align: center;}
.custom button:hover {background: rgba(128, 128, 128, 0.9) !important; box-shadow: 2px 2px black !important;}
.custom button:active {box-shadow: 5px 5px black !important;}
.first button {background-color: rgba(128,128,128,0.5); box-shadow: 0 3px 2px rgba(128,128,128,0.7);}
.first button:focus, .first button:hover {background-color: rgba(128,128,128,0.9);}
.second button {color: blue; border: 1px solid blue; background-color: white;}
.second button:focus, .second button:hover {background-color: rgba(0,0,255,0.1);}
.third button {background-color: white; color: blue;}
.third button:focus, .third button:hover {background-color: rgba(0,0,255,0.1);}
.fourth button {color: white; background-color:blue; box-shadow: none;}
.fifth, .sixth, .seventh, .eighth, .ninth, .tenth, .eleventh, .twelfth, .thirteenth, .fourteenth, .fifteenth { float: left;}
.sixth button {background-color: white;}
.seventh, .ninth, .twelfth {clear: left;}
.seventh button, .eighth button, .ninth button, .tenth button, .eleventh button, .thirteenth button {color: white; background-color: rgba(0, 0, 255, 0.7); box-shadow: 0 3px 2px lightblue;}
.thirteenth button:hover, .thirteenth button:focus {background-color: rgba(0, 0, 255, 1);}
.fourteenth button, .fifteenth button {color: white;}
.fourteenth button {background-color: rgba(0,0,0, 0.8); box-shadow: 0 3px 2px rgba(0,0,0,0.4)}
.fourteenth button:hover, .fourteenth button:focus {background-color: rgba(0,0,0, 1);}
.fifteenth button {background-color: rgba(255,0,0, 0.75); box-shadow: 0 3px 2px rgba(255,0,0,0.4)}
.fifteenth button:hover, .fifteenth button:focus {background-color: rgba(255,0,0, 1);}

footer {padding: 20px; text-align: center; border-top: 1px solid green;}
main {overflow: hidden;}


</style>
