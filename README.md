# vue-composent
### This is a VueJS Project using a custom Dropdown list component, where you can easily set the basic properties to make it works.

## Set the Dropdown List component properties
```xml
<template>
  <Select :items="items"
      placeholder="Choose Something" 
      :multiselect="false"
      :isSmall="false"/>
</template>

```

```js
import Select from './components/Select/Select';

export default {
  name: 'App',
  components: {
    Select
  },
  data () {
    return {
      items: [ 
        {name:'Andres', checked:false},
        {name:'Daniela', checked:false},
        {name:'Rafael', checked:false},

      ]
    }
  }
}
```

## This project is using internaly the font Awesome Library to set the icons. You can use the icons from [Font Awesome](https://fontawesome.com/)

```js
import { library } from '@fortawesome/fontawesome-svg-core'
import { faAmbulance, faBox, faBrain } from '@fortawesome/free-solid-svg-icons'
library.add(faAmbulance, faBox, faBrain)
export default {
    //...
  data () {
    return {
      items: [ 
        {name:'Andres',checked:false, icon:'brain'},
        {name:'Daniela',checked:false, icon:'ambulance'},
        {name:'Rafael',checked:false, icon:'box'},

      ]
    }
  }
  //...
}

```

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```
