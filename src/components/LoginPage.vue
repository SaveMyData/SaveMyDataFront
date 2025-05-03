<template>
  <div class="min-h-screen w-full flex items-center justify-center bg-gray-50">
    <div class="flex w-11/12 max-w-6xl min-h-[600px] rounded-2xl overflow-hidden shadow-xl">
      <!-- Partie gauche avec design moderne -->
      <div class="relative flex-1 flex flex-col items-center justify-center text-center text-white p-10 bg-gradient-to-br from-indigo-900 to-purple-800">
        <!-- Overlay pour assurer la lisibilité du texte -->
        <div class="absolute inset-0 bg-gradient-to-br from-indigo-900/90 to-purple-800/90 z-10"></div>

        <div class="relative z-20 flex flex-col items-center w-full">
          <div class="mb-8">
            <div class="w-20 h-20 rounded-full border-2 border-white/80 flex items-center justify-center bg-white/10">
              <ServerIcon class="w-8 h-8" />
            </div>
          </div>
          <h2 class="text-4xl font-bold mb-2">SaveMyData</h2>
          <p class="text-lg opacity-80 max-w-[80%]">Sécurisez vos documents sensibles</p>
        </div>
      </div>

      <!-- Partie droite avec le formulaire de login -->
      <div class="flex-1 bg-white p-10 md:p-16 flex flex-col">
        <div class="mb-10">
          <h1 class="text-4xl font-bold text-gray-800 mb-2">Bienvenue</h1>
          <p class="text-gray-600 text-lg">Connectez-vous à votre espace sécurisé</p>
        </div>

        <form @submit.prevent="handleLogin" class="flex flex-col gap-6 mb-8">
          <div class="flex flex-col gap-2">
            <label for="username" class="text-sm font-medium text-gray-700">Nom d'utilisateur</label>
            <div class="relative">
              <UserIcon class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5" />
              <input
                  id="username"
                  type="text"
                  v-model="username"
                  placeholder="Entrez votre nom d'utilisateur"
                  required
                  class="w-full py-3.5 pl-12 pr-4 rounded-lg border border-gray-200 bg-gray-50 text-gray-800 focus:outline-none focus:ring-2 focus:ring-pink-500/20 focus:border-pink-500 transition-all"
              />
            </div>
          </div>

          <div class="flex flex-col gap-2">
            <label for="password" class="text-sm font-medium text-gray-700">Mot de passe</label>
            <div class="relative">
              <LockIcon class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5" />
              <input
                  id="password"
                  type="password"
                  v-model="password"
                  placeholder="Entrez votre mot de passe"
                  required
                  class="w-full py-3.5 pl-12 pr-4 rounded-lg border border-gray-200 bg-gray-50 text-gray-800 focus:outline-none focus:ring-2 focus:ring-pink-500/20 focus:border-pink-500 transition-all"
              />
            </div>
          </div>

          <div class="flex gap-4 mt-2 md:flex-row flex-col">
            <button
                type="submit"
                class="flex-1 py-3.5 px-4 rounded-lg bg-pink-600 text-white font-semibold hover:bg-pink-700 transform hover:-translate-y-0.5 transition-all"
            >
              Se connecter
            </button>
            <button
                type="button"
                @click="goToRegister"
                class="flex-1 py-3.5 px-4 rounded-lg border border-pink-600 text-pink-600 font-semibold hover:bg-pink-50 transform hover:-translate-y-0.5 transition-all"
            >
              S'inscrire
            </button>
          </div>
        </form>

        <div class="mt-auto">
          <button class="w-full py-3 px-4 rounded-lg border border-gray-200 bg-white text-gray-700 font-medium flex items-center justify-center gap-3 hover:bg-gray-50 transition-all">
            <img src="https://www.gstatic.com/images/branding/product/1x/googleg_36dp.png" alt="Google" class="w-5 h-5" />
            Se connecter avec Google
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { UserIcon, LockIcon, ServerIcon } from 'lucide-vue-next'

const username = ref('')
const password = ref('')

const handleLogin = () => {
  // Ici vous pouvez implémenter la logique d'authentification
  console.log('Login attempt:', username.value, password.value)

  // Émettre un événement pour informer le parent de la connexion
  emit('login-success', { username: username.value })
}

const goToRegister = () => {
  // Émettre un événement pour naviguer vers la page d'inscription
  emit('navigate', 'register')
}

// Définir les événements pour communiquer avec le composant parent
const emit = defineEmits(['login-success', 'navigate'])
</script>