<script setup>
import { ref, onMounted } from 'vue'

const isHidden = ref(false)

const toggleControls = () => {
  isHidden.value = !isHidden.value
  if (typeof document !== 'undefined') {
    document.documentElement.classList.toggle('hide-slidev-ui', isHidden.value)
    document.documentElement.classList.toggle('show-slidev-ui-mobile', !isHidden.value)
  }
}

// En pantallas de móviles colapsar y ocultar predeterminadamente los controles para no tapar el contenido
onMounted(() => {
  if (typeof window !== 'undefined' && window.innerWidth <= 768) {
    isHidden.value = true
    document.documentElement.classList.add('hide-slidev-ui')
  }
})
</script>

<template>
  <button 
    @click="toggleControls"
    class="custom-ui-toggle-btn"
    :title="isHidden ? 'Mostrar barra de navegación' : 'Ocultar barra de navegación'"
  >
    <span v-if="isHidden">👁️ Mostrar Controles</span>
    <span v-else>👁️‍🗨️ Ocultar Controles</span>
  </button>
</template>

<style>
.custom-ui-toggle-btn {
  position: fixed !important;
  top: 12px !important;
  right: 12px !important;
  z-index: 2147483647 !important; /* Máximo z-index posible para asegurar visibilidad */
  background: rgba(184, 50, 37, 0.85) !important;
  color: #FFFFFF !important;
  border: 1px solid rgba(255, 255, 255, 0.2) !important;
  border-radius: 20px !important;
  padding: 6px 14px !important;
  font-family: 'Inter', sans-serif !important;
  font-size: 0.75rem !important;
  font-weight: 600 !important;
  cursor: pointer !important;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.2) !important;
  backdrop-filter: blur(8px) !important;
  transition: all 0.3s ease !important;
  display: flex !important;
  align-items: center !important;
  gap: 6px !important;
}

.custom-ui-toggle-btn:hover {
  background: #D4654A !important;
  transform: translateY(-1px) !important;
}

/* Ocultar el botón si la presentación está en modo nativo de impresión/exportación */
@media print {
  .custom-ui-toggle-btn {
    display: none !important;
  }
}
</style>
