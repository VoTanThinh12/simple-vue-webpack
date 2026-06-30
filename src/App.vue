<template>
  <div class="app-container">
    <div class="glow-sphere glow-1"></div>
    <div class="glow-sphere glow-2"></div>
    
    <div class="glass-card">
      <div class="badge">Vue 3 + Webpack</div>
      
      <h1 class="title">Hello <span class="gradient-text">{{ message }}</span></h1>
      
      <div class="counter-display">
        <span class="counter-label">Current Count</span>
        <div class="counter-value" :class="{ 'positive': count > 0, 'negative': count < 0 }">
          {{ count }}
        </div>
      </div>
      
      <div class="button-group">
        <button class="btn btn-decrement" @click="handleDes" aria-label="Decrement count">
          <span class="btn-icon">−</span>
          <span class="btn-text">Decrease</span>
        </button>
        <button class="btn btn-increment" @click="handleAdd" aria-label="Increment count">
          <span class="btn-icon">+</span>
          <span class="btn-text">Increase</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const count = ref<number>(0)
const message = 'Vue 3'

const handleAdd = () => count.value++
const handleDes = () => count.value--
</script>

<style lang="less">
/* Reset and Base Styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Outfit', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  background-color: #0b0f19;
  color: #f3f4f6;
  overflow: hidden;
}
</style>

<style scoped lang="less">
.app-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  width: 100vw;
  background: radial-gradient(circle at 50% 50%, #1e1b4b 0%, #09070f 100%);
  position: relative;
  overflow: hidden;
}

/* Background decorative glowing spheres */
.glow-sphere {
  position: absolute;
  border-radius: 50%;
  filter: blur(120px);
  z-index: 1;
  opacity: 0.45;
}

.glow-1 {
  width: 350px;
  height: 350px;
  background: #4f46e5;
  top: -10%;
  left: 15%;
  animation: float-slow 12s ease-in-out infinite alternate;
}

.glow-2 {
  width: 400px;
  height: 400px;
  background: #db2777;
  bottom: -15%;
  right: 10%;
  animation: float-slow 16s ease-in-out infinite alternate-reverse;
}

@keyframes float-slow {
  0% { transform: translateY(0px) scale(1); }
  100% { transform: translateY(40px) scale(1.1); }
}

/* Glassmorphism Card */
.glass-card {
  position: relative;
  z-index: 10;
  width: 100%;
  max-width: 440px;
  padding: 3rem 2.5rem;
  background: rgba(255, 255, 255, 0.03);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 24px;
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5), 
              inset 0 1px 1px rgba(255, 255, 255, 0.1);
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  
  &:hover {
    transform: translateY(-4px);
    box-shadow: 0 30px 60px -10px rgba(0, 0, 0, 0.6), 
                0 0 40px rgba(79, 70, 229, 0.15),
                inset 0 1px 2px rgba(255, 255, 255, 0.2);
  }
}

.badge {
  background: linear-gradient(135deg, rgba(79, 70, 229, 0.15) 0%, rgba(219, 39, 119, 0.15) 100%);
  border: 1px solid rgba(255, 255, 255, 0.1);
  padding: 0.4rem 1.2rem;
  border-radius: 100px;
  font-size: 0.75rem;
  font-weight: 600;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  color: #a5b4fc;
  margin-bottom: 1.5rem;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.title {
  font-size: 2.25rem;
  font-weight: 800;
  margin-bottom: 2rem;
  letter-spacing: -0.02em;
  color: #ffffff;
}

.gradient-text {
  background: linear-gradient(135deg, #818cf8 0%, #f472b6 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

/* Counter Display */
.counter-display {
  width: 100%;
  background: rgba(255, 255, 255, 0.015);
  border: 1px solid rgba(255, 255, 255, 0.04);
  border-radius: 16px;
  padding: 1.5rem;
  margin-bottom: 2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.2);
}

.counter-label {
  font-size: 0.85rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: #9ca3af;
  margin-bottom: 0.5rem;
}

.counter-value {
  font-size: 4rem;
  font-weight: 800;
  font-variant-numeric: tabular-nums;
  line-height: 1;
  color: #ffffff;
  transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
  text-shadow: 0 0 20px rgba(255, 255, 255, 0.1);
  
  &.positive {
    color: #34d399;
    text-shadow: 0 0 25px rgba(52, 211, 153, 0.35);
  }
  
  &.negative {
    color: #f87171;
    text-shadow: 0 0 25px rgba(248, 113, 113, 0.35);
  }
}

/* Control Buttons */
.button-group {
  display: flex;
  gap: 1rem;
  width: 100%;
}

.btn {
  flex: 1;
  outline: none;
  border: none;
  cursor: pointer;
  padding: 1rem;
  border-radius: 14px;
  font-size: 0.95rem;
  font-weight: 600;
  color: #ffffff;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  
  &:active {
    transform: scale(0.96);
  }
}

.btn-decrement {
  background: linear-gradient(135deg, #ef4444 0%, #b91c1c 100%);
  border: 1px solid rgba(239, 68, 68, 0.2);
  
  &:hover {
    background: linear-gradient(135deg, #f87171 0%, #dc2626 100%);
    box-shadow: 0 0 20px rgba(239, 68, 68, 0.35);
    transform: translateY(-2px);
  }
}

.btn-increment {
  background: linear-gradient(135deg, #10b981 0%, #047857 100%);
  border: 1px solid rgba(16, 185, 129, 0.2);
  
  &:hover {
    background: linear-gradient(135deg, #34d399 0%, #059669 100%);
    box-shadow: 0 0 20px rgba(16, 185, 129, 0.35);
    transform: translateY(-2px);
  }
}

.btn-icon {
  font-size: 1.25rem;
  line-height: 1;
}

@media (max-width: 480px) {
  .glass-card {
    padding: 2rem 1.5rem;
  }
  
  .title {
    font-size: 1.75rem;
  }
  
  .counter-value {
    font-size: 3rem;
  }
}
</style>

