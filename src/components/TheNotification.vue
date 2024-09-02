<template>
  <transition name="fade">
    <div v-if="visible" :class="['notification', typeClass]">
      <img :src="iconSrc" alt="Icon" class="notification-icon" />
      <div class="notification-content">
        <h2>{{ titulo }}</h2>
        <p>{{ subtitulo }}</p>
      </div>
    </div>
  </transition>
</template>

<script setup>
import { ref, computed } from 'vue';


const props = defineProps({
  titulo: {
    type: String,
    default: 'Título Padrão'
  },
  subtitulo: {
    type: String,
    default: 'Subtítulo Padrão'
  },
  timeout: {
    type: Number,
    default: 3000
  },
  type: {
    type: String,
    default: 'success',
    validator: (value) => ['success', 'error'].includes(value)
  }
});


const visible = ref(false);

const typeClass = computed(() => {
  return props.type === 'success' ? 'notification-success' : 'notification-error';
});
 
const iconSrc = computed(() => {
  return props.type === 'success'
    ? 'https://img.icons8.com/color/48/000000/checkmark.png'
    : 'https://img.icons8.com/color/48/000000/error--v1.png';
});


const setNotification = (newTitulo, newSubtitulo, newType = 'success', customTimeout = props.timeout) => {
  props.titulo = newTitulo;
  props.subtitulo = newSubtitulo;
  props.type = newType;
  visible.value = true;

  setTimeout(() => {
    visible.value = false;
  }, customTimeout);
};


defineExpose({
  setNotification
});
</script>

<style scoped>
.notification {
  display: flex;
  align-items: center;
  padding: 15px;
  border-radius: 5px;
  margin: 10px 0;
  color: #fff;
  transition: all 1s ease;
  margin: 0 auto;
}


.notification-success {
  background-color: #4caf50;
}


.notification-error {
  background-color: #f44336; 
}

.notification-icon {
  width: 40px;
  height: 40px;
  margin-right: 15px;
}

.notification-content h2 {
  margin: 0;
  font-size: 1.2em;
}

.notification-content p {
  margin: 5px 0 0 0;
  font-size: 1em;
}

/* Transições */
.fade-enter-active, .fade-leave-active {
  transition: all 1s ease;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
.fade-enter-to, .fade-leave {
  opacity: 1;
  transform: translateY(10px);
}
</style>
