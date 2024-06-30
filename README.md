# my-project-vue

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

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
# VueResponsiveNavbar

1. Instalar Font Awesome
Primero, necesitas instalar Font Awesome en tu proyecto:

bash
Copiar código
npm install @fortawesome/fontawesome-free
2. Importar Font Awesome en tu proyecto
Debes importar los estilos de Font Awesome en tu archivo main.js:

javascript
Copiar código
// src/main.js
import { createApp } from 'vue'
import App from './App.vue'
import '@fortawesome/fontawesome-free/css/all.css'

createApp(App).mount('#app')
