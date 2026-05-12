# 🧠 Identificación de Señales de Riesgo — Presentación Slidev

Presentación profesional sobre identificación de señales de riesgo en adolescentes y jóvenes, creada por la **Psicóloga Ingrid Cabalin**.

## 📦 Instalación

```bash
npm install
```

## 🚀 Ejecución en modo desarrollo

```bash
npm run dev
```

Se abrirá automáticamente en `http://localhost:3030`

## 🖥️ Modo Presentador

Presiona la tecla **P** durante la presentación para abrir la vista de presentador con notas y previsualización.

## 📱 Modo Remoto (controlar desde teléfono)

```bash
npm run remote
```

Esto habilita el control remoto. Escanea el código QR o accede a la URL mostrada en consola desde tu teléfono para controlar la presentación remotamente.

## 🎯 Navegación

| Acción | Tecla |
|--------|-------|
| Siguiente slide | `→` `↓` `Espacio` `Click` |
| Slide anterior | `←` `↑` |
| Vista general | `O` |
| Modo presentador | `P` |
| Modo oscuro | `D` (toggle) |
| Pantalla completa | `F` |

> ✅ Compatible con **clickers de presentación** (envían señales de flechas).

## 📂 Estructura del Proyecto

```
├── slides.md              # Contenido de las 10 diapositivas
├── components/
│   └── RiskLevelExplorer.vue  # Componente interactivo Vue 3
├── styles/
│   └── global.css         # Sistema de diseño (tokens, tipografía, layouts)
├── public/                # Imágenes ilustrativas
├── package.json           # Dependencias y scripts
└── README.md              # Este archivo
```

## 🎨 Decisiones de Diseño

- **Paleta cálida**: Tonos arena (#F5EDE3), terracotta (#B83225) y pasteles suaves, generando empatía y calidez.
- **Tipografía**: Playfair Display (títulos) + Inter (cuerpo) para equilibrio entre autoridad y legibilidad.
- **Transiciones fade**: Elegantes y no distractoras, apropiadas para contenido sensible.
- **Componente interactivo**: Termómetro de niveles de riesgo que permite explorar la diferenciación entre desarrollo normal, señales de riesgo y alertas urgentes.

## 📤 Exportar a PDF

```bash
npm run export
```

## 🏗️ Build para producción

```bash
npm run build
```
