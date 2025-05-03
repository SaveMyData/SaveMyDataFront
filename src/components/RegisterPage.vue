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

      <!-- Partie droite avec le formulaire d'inscription -->
      <div class="flex-1 bg-white p-10 md:p-16 flex flex-col">
        <div class="mb-8">
          <h1 class="text-4xl font-bold text-gray-800 mb-2">Créer un compte</h1>
          <p class="text-gray-600 text-lg">Rejoignez-nous pour sécuriser vos documents</p>
        </div>

        <form @submit.prevent="handleRegister" class="flex flex-col gap-5 mb-6">
          <div class="flex flex-col gap-2">
            <label for="fullname" class="text-sm font-medium text-gray-700">Nom complet</label>
            <div class="relative">
              <UserIcon class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5" />
              <input
                  id="fullname"
                  type="text"
                  v-model="fullname"
                  placeholder="Entrez votre nom complet"
                  required
                  class="w-full py-3.5 pl-12 pr-4 rounded-lg border border-gray-200 bg-gray-50 text-gray-800 focus:outline-none focus:ring-2 focus:ring-pink-500/20 focus:border-pink-500 transition-all"
              />
            </div>
          </div>

          <div class="flex flex-col gap-2">
            <label for="email" class="text-sm font-medium text-gray-700">Adresse email</label>
            <div class="relative">
              <MailIcon class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5" />
              <input
                  id="email"
                  type="email"
                  v-model="email"
                  placeholder="Entrez votre adresse email"
                  required
                  class="w-full py-3.5 pl-12 pr-4 rounded-lg border border-gray-200 bg-gray-50 text-gray-800 focus:outline-none focus:ring-2 focus:ring-pink-500/20 focus:border-pink-500 transition-all"
              />
            </div>
          </div>

          <div class="flex flex-col gap-2">
            <label for="username" class="text-sm font-medium text-gray-700">Nom d'utilisateur</label>
            <div class="relative">
              <AtSignIcon class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5" />
              <input
                  id="username"
                  type="text"
                  v-model="username"
                  placeholder="Choisissez un nom d'utilisateur"
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
                  placeholder="Créez un mot de passe sécurisé"
                  required
                  class="w-full py-3.5 pl-12 pr-4 rounded-lg border border-gray-200 bg-gray-50 text-gray-800 focus:outline-none focus:ring-2 focus:ring-pink-500/20 focus:border-pink-500 transition-all"
              />
            </div>
          </div>

          <div class="flex flex-col gap-2">
            <label for="confirmPassword" class="text-sm font-medium text-gray-700">Confirmer le mot de passe</label>
            <div class="relative">
              <ShieldCheckIcon class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5" />
              <input
                  id="confirmPassword"
                  type="password"
                  v-model="confirmPassword"
                  placeholder="Confirmez votre mot de passe"
                  required
                  class="w-full py-3.5 pl-12 pr-4 rounded-lg border border-gray-200 bg-gray-50 text-gray-800 focus:outline-none focus:ring-2 focus:ring-pink-500/20 focus:border-pink-500 transition-all"
              />
            </div>
            <p v-if="passwordError" class="text-red-500 text-sm mt-1">{{ passwordError }}</p>
          </div>

          <div class="flex items-center mt-2">
            <input
                id="terms"
                type="checkbox"
                v-model="acceptTerms"
                class="h-4 w-4 text-pink-600 focus:ring-pink-500 border-gray-300 rounded"
            />
            <label for="terms" class="ml-2 block text-sm text-gray-700">
              J'accepte les <a href="#" class="text-pink-600 hover:underline">conditions d'utilisation</a> et la <a href="#" class="text-pink-600 hover:underline">politique de confidentialité</a>
            </label>
          </div>

          <div class="flex gap-4 mt-4 md:flex-row flex-col">
            <button
                type="submit"
                class="flex-1 py-3.5 px-4 rounded-lg bg-pink-600 text-white font-semibold hover:bg-pink-700 transform hover:-translate-y-0.5 transition-all disabled:opacity-70 disabled:cursor-not-allowed disabled:hover:transform-none"
                :disabled="!isFormValid"
            >
              Créer mon compte
            </button>
            <button
                type="button"
                @click="goToLogin"
                class="flex-1 py-3.5 px-4 rounded-lg border border-pink-600 text-pink-600 font-semibold hover:bg-pink-50 transform hover:-translate-y-0.5 transition-all"
            >
              Déjà inscrit ? Se connecter
            </button>
          </div>
        </form>

        <div class="mt-auto">
          <button class="w-full py-3 px-4 rounded-lg border border-gray-200 bg-white text-gray-700 font-medium flex items-center justify-center gap-3 hover:bg-gray-50 transition-all">
            <img src="https://www.gstatic.com/images/branding/product/1x/googleg_36dp.png" alt="Google" class="w-5 h-5" />
            S'inscrire avec Google
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { UserIcon, LockIcon, ServerIcon, MailIcon, AtSignIcon, ShieldCheckIcon } from 'lucide-vue-next'

const fullname = ref('')
const email = ref('')
const username = ref('')
const password = ref('')
const confirmPassword = ref('')
const acceptTerms = ref(false)

const passwordError = computed(() => {
  if (password.value && confirmPassword.value && password.value !== confirmPassword.value) {
    return 'Les mots de passe ne correspondent pas'
  }
  return ''
})

const isFormValid = computed(() => {
  return fullname.value &&
      email.value &&
      username.value &&
      password.value &&
      confirmPassword.value &&
      password.value === confirmPassword.value &&
      acceptTerms.value
})

const handleRegister = () => {
  if (!isFormValid.value)
    return

  console.log('Register attempt:', {
    fullname: fullname.value,
    email: email.value,
    username: username.value,
    password: password.value
  })
  // Call API to register the user

  emit('navigate', 'dashboard')
}

const goToLogin = () => {
  // Émettre un événement pour naviguer vers la page de connexion
  emit('navigate', 'login')
}

// Définir les événements pour communiquer avec le composant parent
const emit = defineEmits(['register-success', 'navigate'])
</script>