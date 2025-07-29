# 🌱 Documento Vue 3 contemplado recursos utilizados na implementação do simulador de salários  

Este documento apresenta de forma sucinta os principais conceitos do **Vue 3** aliados ao **Vite** (empacotador moderno) e ao **Bootstrap** (framework CSS), com exemplos práticos de **componentes, rotas, views, emits e computed properties**.  

---

## 🚀 1. Criando o projeto com Vite  

O **Vite** é o empacotador recomendado para Vue 3 por ser extremamente rápido, simples e otimizado para desenvolvimento moderno. Ele oferece *hot reload* imediato e configuração mínima.  

```bash
# Criação do projeto
npm create vite@latest meu-projeto-vue
cd meu-projeto-vue
npm install

# Instalação do Bootstrap
npm install bootstrap
```

No arquivo `main.js` importe o Bootstrap:  

```js
import { createApp } from 'vue'
import App from './App.vue'
import 'bootstrap/dist/css/bootstrap.min.css'

createApp(App).mount('#app')
```

---

## 🎨 2. Estilização com Bootstrap  

O **Bootstrap** é um dos frameworks CSS mais usados no mundo. Ele fornece **classes utilitárias** e **componentes prontos** (botões, cards, formulários, grids) que facilitam a criação de interfaces responsivas e bem estruturadas. Neste projeto, o **Bootstrap** foi utilizado para adicionar estilo e responsividade ao simulador de salários.

### Exemplos de classes úteis utilizadas:  

| Classe | Função |
|--------|---------|
| `container`, `row`, `col` | Layout responsivo |
| `btn`, `btn-primary`, `btn-danger` | Botões estilizados |
| `form-control` | Formulários estilizados |

---

## 🧩 3. Estrutura de Componentes  

No Vue 3, tudo gira em torno de **componentes reutilizáveis**. Eles encapsulam lógica, estilo e template em um único arquivo `.vue`. Componentes recebem **props** (dados vindos do pai) e podem emitir eventos para se comunicar de volta. Isso facilita a organização da aplicação e promove reutilização de código.  

Os **emits** permitem que um componente filho envie informações ou dispare ações para o componente pai. Isso segue o padrão de comunicação **pai → filho (via props)** e **filho → pai (via emits)**, mantendo a hierarquia clara e a aplicação mais previsível. Assim, por exemplo, um botão em um componente filho pode avisar ao pai que foi clicado, passando até mesmo valores ou identificadores.  

### Exemplo: `src/components/CardInfo.vue`  

```vue
<template>
  <div class="card p-3 m-2">
    <h5>{{ title }}</h5>
    <p>{{ description }}</p>
    <button class="btn btn-primary" @click="$emit('show-details', id)">
      Detalhes
    </button>
  </div>
</template>

<script setup>
defineProps({
  id: Number,
  title: String,
  description: String
})

defineEmits(['show-details'])
</script>
```

---

## 📄 4. Views e Rotas  

O **Vue Router** é a biblioteca oficial para navegação entre páginas no Vue. Ele trabalha com o conceito de **rotas** (URLs que apontam para componentes específicos chamados de *views*). Isso permite estruturar a aplicação em múltiplas páginas, cada uma carregando um componente diferente.  

### Instalação  

```bash
npm install vue-router
```

### Configuração: `src/router/index.js`  

```js
import { createRouter, createWebHistory } from 'vue-router'
import HomeView from '../views/HomeView.vue'
import AboutView from '../views/AboutView.vue'

const routes = [
  { path: '/', component: HomeView },
  { path: '/about', component: AboutView }
]

export default createRouter({
  history: createWebHistory(),
  routes
})
```

### Registro no `main.js`  

```js
import router from './router'
createApp(App).use(router).mount('#app')
```

### Exemplo de View: `src/views/HomeView.vue`  

```vue
<template>
  <div class="container mt-4">
    <h2>Página Inicial</h2>
    <CardInfo
      v-for="item in items"
      :key="item.id"
      v-bind="item"
      @show-details="verDetalhes"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import CardInfo from '../components/CardInfo.vue'

const items = ref([
  { id: 1, title: "Vue 3", description: "Framework progressivo" },
  { id: 2, title: "Vite", description: "Empacotador rápido" }
])

function verDetalhes(id) {
  alert("Você clicou no item " + id)
}
</script>
```

---

## 🧮 5. Computed Properties  

As **computed properties** são propriedades derivadas do estado reativo. Elas permitem calcular valores dinamicamente a partir de outras variáveis, evitando duplicação de lógica e garantindo performance, já que são **cacheadas** até que suas dependências mudem.  

🔹 Ideal para: formatar textos, aplicar cálculos, filtrar listas e qualquer transformação de dados.  

### Exemplo: `src/views/AboutView.vue`  

```vue
<template>
  <div class="container mt-4">
    <h2>Sobre</h2>
    <input v-model="nome" class="form-control" placeholder="Digite seu nome">
    <p class="mt-2">Olá, <strong>{{ nomeFormatado }}</strong>!</p>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const nome = ref('')

const nomeFormatado = computed(() =>
  nome.value.trim() === '' ? 'Visitante' : nome.value.toUpperCase()
)
</script>
```

---



## ✅ Conclusão  

Este documento apresentou detalhes e exemplos dos recursos do Vue 3 utilizados na implementação do simulador de salários, contemplando:  
- 🔹 **Componentes** com `props` e `emit` para comunicação.  
- 🔹 **Bootstrap** para estilização rápida e responsiva.  
- 🔹 **Rotas e Views** com `vue-router` para navegação.  
- 🔹 **Computed properties** para cálculos reativos.  
- 🔹 **Vite** como empacotador do projeto.  

---
