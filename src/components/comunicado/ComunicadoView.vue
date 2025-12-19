<template>
  <div class="min-h-screen bg-gradient-to-br from-[#80006A] via-[#A65C99] to-[#FF5F3F] flex items-center justify-center p-4 font-sans">
    <!-- Elementos decorativos de fondo -->
    <div class="absolute inset-0 overflow-hidden">
      <div class="absolute -top-20 -right-20 w-72 h-72 bg-white/10 rounded-full blur-3xl animate-pulse"></div>
      <div class="absolute -bottom-20 -left-20 w-80 h-80 bg-blue-900/20 rounded-full blur-3xl animate-pulse delay-1000"></div>
    </div>

    <!-- Tarjeta de Comunicado -->
    <div class="relative z-10 w-full max-w-lg transform transition-all duration-500 ease-out" :class="cardVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'">
      <div class="bg-white/90 dark:bg-gray-900/80 backdrop-blur-xl rounded-2xl shadow-2xl p-8 md:p-12 border border-white/20">
        
        <!-- Encabezado -->
        <div class="text-center mb-8">
          <div class="inline-flex items-center justify-center w-16 h-16 bg-gradient-to-br from-purple-600 to-pink-500 rounded-2xl mb-6 shadow-lg">
            <MegaphoneIcon class="w-8 h-8 text-white" />
          </div>
          <h1 class="text-3xl md:text-4xl font-bold text-gray-900 dark:text-white mb-2">
            Anuncio Importante
          </h1>
          <p class="text-base text-gray-600 dark:text-gray-400">
            Nuestra plataforma se ha movido a una nueva dirección.
          </p>
        </div>

        <!-- Cuerpo del Mensaje -->
        <div class="space-y-6 text-center">
          <p class="text-gray-700 dark:text-gray-300">
            Para mejorar tu experiencia y ofrecer un servicio más robusto, hemos migrado nuestro tablero de control a una nueva y moderna plataforma.
          </p>
          
          <div>
            <p class="text-sm font-semibold text-gray-800 dark:text-gray-200 mb-3">
              A partir de ahora, por favor accede a través de la siguiente dirección:
            </p>
            
            <!-- Campo de URL con botón de copiar -->
            <div class="relative flex items-center">
              <input
                :value="newUrl"
                readonly
                class="w-full pl-4 pr-16 py-3 bg-gray-100 dark:bg-gray-800 text-gray-700 dark:text-gray-300 border-2 border-gray-200 dark:border-gray-700 rounded-lg font-mono text-sm focus:outline-none"
              />
              <button @click="copyToClipboard" class="absolute right-2 top-1/2 -translate-y-1/2 px-3 py-1.5 bg-gray-200 dark:bg-gray-700 text-gray-600 dark:text-gray-300 hover:bg-gray-300 dark:hover:bg-gray-600 rounded-md text-xs font-semibold transition-all duration-200 flex items-center gap-1">
                <CopyIcon v-if="!copySuccess" class="w-3.5 h-3.5" />
                <CheckIcon v-else class="w-3.5 h-3.5 text-green-500" />
                {{ copySuccess ? 'Copiado' : 'Copiar' }}
              </button>
            </div>
          </div>
          
          <p class="text-xs text-gray-500 dark:text-gray-500">
            Por favor, actualiza tus marcadores y accesos directos.
          </p>
        </div>

        <!-- Botón de Acción -->
        <div class="mt-10">
          <a
            :href="newUrl"
            target="_blank"
            class="w-full flex items-center justify-center gap-3 px-6 py-4 bg-gradient-to-r from-[#80006A] to-[#FF5F3F] text-white font-bold rounded-xl shadow-lg transform transition-all duration-300 hover:scale-105 hover:shadow-2xl focus:outline-none focus:ring-4 focus:ring-pink-300 dark:focus:ring-pink-800"
          >
            <span>Ir a la Nueva Plataforma</span>
            <MoveRightIcon class="w-5 h-5" />
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { MegaphoneIcon, CopyIcon, CheckIcon, MoveRightIcon } from 'lucide-vue-next';

const newUrl = ref('https://tablerocontrolzentria.netlify.app');
const copySuccess = ref(false);
const cardVisible = ref(false);

onMounted(() => {
  document.title = 'Aviso Importante'
  // Para la animación de entrada
  setTimeout(() => {
    cardVisible.value = true;
  }, 100);
});

const copyToClipboard = async () => {
  try {
    await navigator.clipboard.writeText(newUrl.value);
    copySuccess.value = true;
    setTimeout(() => {
      copySuccess.value = false;
    }, 2000);
  } catch (err) {
    console.error('Error al copiar la URL:', err);
    alert('No se pudo copiar la URL.');
  }
};
</script>

<style scoped>
/* Estilos adicionales si fueran necesarios */
</style>
