<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import TheNotification from './components/TheNotification.vue';
import { ref, onMounted } from 'vue';

onMounted(() => {
  setTimeout(() => {
    notificationRef.value.setNotification();
  }, 2000);
});

const notificationRef = ref(null);
</script>

<template>
  <header>
    <!-- <TheNotification ref="notificationRef" titulo="Sucesso!" subtitulo="A operação foi concluída com sucesso." type="success" timeout="5000" /> -->

    <TheNotification ref="notificationRef" titulo="Erro!" subtitulo="Houve um problema ao processar a operação." type="error" timeout="5000" />

    <!-- <TheNotification ref="notificationRef" titulo="Parabéns" subtitulo="Seu primeiro acesso foi registrado" timeout="5000" /> -->
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />
    <!-- <TheNotification titulo="Custom Title" subtitulo="Custom Subtitle" timeout="5000" /> -->
     <div>
      <!-- <TheNotification ref="notificationRef" titulo="Custom Title" subtitulo="Custom Subtitle" timeout="5000" /> -->
      <!-- <button @click="showNotification">Mostrar Notificação</button> -->
    </div>
    <div class="wrapper">
      <HelloWorld msg="TESTING" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
