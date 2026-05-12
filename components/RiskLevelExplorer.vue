<!--
  RiskLevelExplorer.vue
  Componente interactivo que visualiza los 3 niveles de riesgo:
  Normal (desarrollo) → Señales de Riesgo → Alerta Urgente
  Permite al usuario explorar cada nivel haciendo clic en el termómetro.
-->
<script setup>
import { ref, computed } from 'vue'

const activeLevel = ref(null)

const levels = [
  {
    id: 'normal',
    label: 'Desarrollo Normal',
    color: '#7FAD90',
    colorLight: '#A8D4B5',
    icon: '🌱',
    description: 'Comportamientos esperables en la adolescencia que forman parte del proceso natural de crecimiento.',
    signals: [
      'Cambios físicos y hormonales',
      'Búsqueda de identidad',
      'Necesidad de autonomía',
      'Intensidad emocional',
      'Importancia del grupo de pares',
      'Exploración de intereses'
    ]
  },
  {
    id: 'risk',
    label: 'Señales de Riesgo',
    color: '#E88D7A',
    colorLight: '#F2B5A8',
    icon: '⚠️',
    description: 'Indicadores que requieren atención, observación activa y posible intervención profesional.',
    signals: [
      'Cambios bruscos de ánimo',
      'Aislamiento social importante',
      'Bajo rendimiento escolar',
      'Alteraciones del sueño o apetito',
      'Conductas impulsivas o de riesgo',
      'Consumo de sustancias'
    ]
  },
  {
    id: 'urgent',
    label: 'Alerta Urgente',
    color: '#8B2252',
    colorLight: '#B84578',
    icon: '🚨',
    description: 'Señales que requieren acción inmediata. Buscar ayuda profesional de urgencia.',
    signals: [
      'Expresiones sobre no querer vivir',
      'Autolesiones visibles',
      'Ideación o plan suicida',
      'Cambios extremos de conducta',
      'Regalos de pertenencias valiosas',
      'Despedidas inusuales'
    ]
  }
]

const selectedLevel = computed(() => {
  return levels.find(l => l.id === activeLevel.value) || null
})

function selectLevel(id) {
  activeLevel.value = activeLevel.value === id ? null : id
}
</script>

<template>
  <div class="risk-explorer">
    <!-- Termómetro Visual -->
    <div class="thermometer-section">
      <div class="thermometer">
        <div
          v-for="(level, index) in [...levels].reverse()"
          :key="level.id"
          class="thermo-segment"
          :class="{ active: activeLevel === level.id }"
          :style="{
            '--segment-color': level.color,
            '--segment-color-light': level.colorLight
          }"
          @click="selectLevel(level.id)"
        >
          <span class="thermo-icon">{{ level.icon }}</span>
          <span class="thermo-label">{{ level.label }}</span>
        </div>
      </div>
      <p class="instruction">
        <span class="pulse-dot"></span>
        Haz clic en cada nivel para explorar
      </p>
    </div>

    <!-- Panel de Detalle -->
    <div class="detail-section">
      <transition name="detail-fade" mode="out-in">
        <div v-if="selectedLevel" :key="selectedLevel.id" class="detail-card" :style="{ '--card-color': selectedLevel.color, '--card-color-light': selectedLevel.colorLight }">
          <div class="detail-header">
            <span class="detail-icon">{{ selectedLevel.icon }}</span>
            <h3 class="detail-title">{{ selectedLevel.label }}</h3>
          </div>
          <p class="detail-description">{{ selectedLevel.description }}</p>
          <ul class="detail-signals">
            <li v-for="(signal, i) in selectedLevel.signals" :key="i" :style="{ animationDelay: `${i * 0.07}s` }">
              {{ signal }}
            </li>
          </ul>
        </div>
        <div v-else class="detail-placeholder">
          <div class="placeholder-icon">👆</div>
          <p>Selecciona un nivel del termómetro para ver las señales correspondientes</p>
        </div>
      </transition>
    </div>
  </div>
</template>

<style scoped>
.risk-explorer {
  display: grid;
  grid-template-columns: 260px 1fr;
  gap: 2rem;
  height: 100%;
  align-items: center;
  font-family: 'Inter', sans-serif;
}

/* --- Thermometer --- */
.thermometer-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}

.thermometer {
  display: flex;
  flex-direction: column;
  gap: 6px;
  width: 100%;
}

.thermo-segment {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.9rem 1rem;
  border-radius: 12px;
  cursor: pointer;
  background: rgba(255, 255, 255, 0.5);
  border: 2px solid transparent;
  transition: all 0.35s cubic-bezier(0.4, 0, 0.2, 1);
  user-select: none;
}

.thermo-segment:hover {
  background: rgba(255, 255, 255, 0.8);
  border-color: var(--segment-color-light);
  transform: translateX(4px);
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.06);
}

.thermo-segment.active {
  background: var(--segment-color-light);
  border-color: var(--segment-color);
  transform: translateX(8px);
  box-shadow: 0 6px 24px rgba(0, 0, 0, 0.1);
}

.thermo-icon {
  font-size: 1.4rem;
  flex-shrink: 0;
}

.thermo-label {
  font-size: 0.82rem;
  font-weight: 600;
  color: #4A4A4A;
  line-height: 1.2;
}

.thermo-segment.active .thermo-label {
  color: #2D2D2D;
}

.instruction {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.7rem;
  color: #999;
  font-style: italic;
}

.pulse-dot {
  width: 6px;
  height: 6px;
  background: #E88D7A;
  border-radius: 50%;
  animation: pulse-anim 1.5s infinite;
}

@keyframes pulse-anim {
  0%, 100% { opacity: 0.4; transform: scale(1); }
  50% { opacity: 1; transform: scale(1.3); }
}

/* --- Detail Panel --- */
.detail-section {
  height: 100%;
  display: flex;
  align-items: center;
}

.detail-card {
  background: rgba(255, 255, 255, 0.6);
  border-radius: 16px;
  padding: 1.5rem;
  border: 1px solid rgba(0, 0, 0, 0.04);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.06);
  width: 100%;
  border-top: 3px solid var(--card-color);
}

.detail-header {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  margin-bottom: 0.75rem;
}

.detail-icon {
  font-size: 1.8rem;
}

.detail-title {
  font-family: 'Playfair Display', serif !important;
  font-size: 1.3rem !important;
  font-weight: 700 !important;
  color: var(--card-color) !important;
  margin: 0 !important;
}

.detail-description {
  font-size: 0.85rem;
  color: #6B6B6B;
  line-height: 1.5;
  margin-bottom: 1rem;
  padding-bottom: 0.75rem;
  border-bottom: 1px solid rgba(0, 0, 0, 0.06);
}

.detail-signals {
  list-style: none !important;
  padding: 0 !important;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0.35rem 1rem;
}

.detail-signals li {
  font-size: 0.78rem;
  color: #4A4A4A;
  padding: 0.3rem 0;
  padding-left: 1.2em !important;
  position: relative;
  animation: signalFadeIn 0.4s ease-out both;
  margin-bottom: 0 !important;
}

.detail-signals li::before {
  content: '' !important;
  position: absolute;
  left: 0;
  top: 0.55em;
  width: 6px !important;
  height: 6px !important;
  background: var(--card-color) !important;
  border-radius: 50%;
  opacity: 0.6;
}

@keyframes signalFadeIn {
  from {
    opacity: 0;
    transform: translateX(-8px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

/* --- Placeholder --- */
.detail-placeholder {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 3rem;
  opacity: 0.5;
  width: 100%;
}

.placeholder-icon {
  font-size: 2.5rem;
  margin-bottom: 1rem;
  animation: bounce 2s infinite;
}

@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-8px); }
}

.detail-placeholder p {
  font-size: 0.9rem;
  color: #999;
  max-width: 280px;
  line-height: 1.5;
}

/* --- Transition --- */
.detail-fade-enter-active,
.detail-fade-leave-active {
  transition: all 0.3s ease;
}

.detail-fade-enter-from {
  opacity: 0;
  transform: translateY(12px);
}

.detail-fade-leave-to {
  opacity: 0;
  transform: translateY(-12px);
}
</style>
