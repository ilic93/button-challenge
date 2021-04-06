<template>
  <div>
    <code>{{ title }}</code>
    <br>
    <button :disabled="shouldDisableButton()" :class="sizeClass()" id="mainButton" @click="toggleForm()">
      <span v-if="shouldLeftIcon()" class="material-icons">{{ newLeftIcon || 'help'}}</span>
      {{ newName ? newName : disable ? 'Disabled' : color ? color : 'Default'}}
      <span v-if="shouldRightIcon()" class="material-icons">{{ newRightIcon || 'help'}}</span>
    </button>
    <form name="buttonForm" v-if="customizable" @submit.prevent="updateButton()">
      <label>Label:</label>
      <input name="newName" placeholder="Enter name"/> 
      <br>
      <label>Type:</label>
      <select name="variant">
        <option value="default">Default</option>
        <option value="outline">Outline</option>
        <option value="text">Text</option>
      </select> 
      <br>
      <label>Disable:</label>
      <input type="checkbox" name="checkDisable" value="true"/> 
      <br>
      <label>Disable shadow:</label>
      <input type="checkbox" name="checkDisableShadow" value="true"/>
      <br>
      <label>Color of shadow:</label>
      <input type="color" name="shadowColor"/>
      <br>
      <label>Icons:</label>
      <input type="checkbox" name="leftIcon" value="true"/> Left
      <select name="leftIconSelect">
        <option value="help">help icon</option>
        <option value="list">list icon</option>
        <option value="label">label icon</option>
        <option value="send">send icon</option>
        <option value="launch">launch icon</option>
      </select>
      <input type="checkbox" name="rightIcon" value="true"/> Right
      <select name="rightIconSelect">
        <option value="help">help icon</option>
        <option value="list">list icon</option>
        <option value="label">label icon</option>
        <option value="send">send icon</option>
        <option value="launch">launch icon</option>
      </select>
      <br>
      <label>Size:</label>
      <select name="newSize">
        <option value="small">Small</option>
        <option value="middle" selected>Middle</option>
        <option value="large">Large</option>
      </select> 
      <br>
      <label>Background color:</label>
      <input type="color" name="newBackColor" value="#808080"/>
      <label>Label color:</label>
      <input type="color" name="newLabelColor"/>
      <br>
      <input type="submit" value="submit">
    </form>
  </div>
</template>

<script>

export default {
  props: ['title', 'mustDisable', 'mustLeftIcon', 'mustRightIcon', 'size', 'color', 'customizable'],
  data() {
    return {
      formActive: true,
      newName: '',
      newLeftIcon: '',
      newRightIcon: '',
      newSize: '',
      newBackColor: '',
      disable: false,
      leftIcon: false,
      rightIcon: false
    }
  },
  methods: {
    sizeClass() {
      let sizeClass = this.size == 'lg' ? 'large' : this.size == 'sm' ? 'small' : ''
      return sizeClass
    },
    shouldDisableButton() {
      const x = this.mustDisable ? this.mustDisable : this.disable
      return x
    },
    shouldLeftIcon() {
      const x = this.mustLeftIcon ? this.mustLeftIcon : this.leftIcon
      return x
    },
    shouldRightIcon() {
      const x = this.mustRightIcon ? this.mustRightIcon : this.rightIcon
      return x
    },
    toggleForm() {
      this.formActive = !this.formActive
      if(this.formActive) {
        document.querySelector('form').style.opacity = 1
      } else {
        document.querySelector('form').style.opacity = 0
      }
    },
    updateButton() {
      this.newName = document.buttonForm.newName.value || null

      const variant = document.buttonForm.variant.value
      let variantList = ['default', 'outline', 'text']
      const index = variantList.indexOf(variant)
      variantList.splice(index, 1)
      document.querySelector('#mainButton').classList.add(variant)
      document.querySelector('#mainButton').classList.remove(...variantList)

      this.disable = document.buttonForm.checkDisable.checked

      if(document.buttonForm.checkDisableShadow.checked) {
        document.querySelector('div > button').style.boxShadow = 'none'
      } else {
        const color = document.buttonForm.shadowColor.value
        document.querySelector('div > button').style.boxShadow = `2px 2px ${color}`
      }

      this.leftIcon = document.buttonForm.leftIcon.checked ? true : false
      this.rightIcon = document.buttonForm.rightIcon.checked ? true : false
      this.newLeftIcon = document.buttonForm.leftIconSelect.value
      this.newRightIcon = document.buttonForm.rightIconSelect.value

      const newSize = document.buttonForm.newSize.value
      let sizeList = ['small', 'middle', 'large']
      const index2 = sizeList.indexOf(newSize)
      sizeList.splice(index2, 1)
      document.querySelector('#mainButton').classList.add(newSize)
      document.querySelector('#mainButton').classList.remove(...sizeList)

      const newBackColor = document.buttonForm.newBackColor.value
      document.querySelector('div > button').style.backgroundColor = newBackColor
    
      const newLabelColor = document.buttonForm.newLabelColor.value
      document.querySelector('div > button').style.color = newLabelColor
    }
  }
}
</script>

<style>

div {
  margin-bottom: 15px;
  padding-left: 20px;
  text-align: left;
}
code {
  font-size: 14px;
  margin-bottom: 10px;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  border: 0;
  border-radius: 5px;
  margin-bottom: 5px;
}

button:active {box-shadow: 5px 5px black !important;}

.default {
  border: 0;
  background-color: rgba(128,128,128,0.5);;
}

.outline { 
  border: 1px solid blue; 
  background-color: white;
}

.text {
  border: 0;
  background-color: white;
}

.large {
  padding: 15px 30px;
  font-size: 20px;
}

.small {
  padding: 5px 10px;
  font-size: 12px;
}

.middle {
  padding: 10px 20px;
  font-size: 16px;
}

button:focus, button:hover {cursor: pointer;}
button:disabled {cursor:not-allowed;}
.material-icons {vertical-align: middle;}

form {
  border: 2px solid purple;
  border-radius: 20px;
  padding: 10px;
  width: 50%;
  margin: 0 auto;
  transition: opacity 1s;
  
}
label, select, input[type="color"] {margin-right: 10px;}

</style>