<template>
  <div class="min-h-screen bg-gray-50 flex flex-col">
    <!-- Barre de navigation supérieure -->
    <header class="bg-white border-b border-gray-200 shadow-sm">
      <div class="flex items-center justify-between px-4 py-3">
        <div class="flex items-center gap-3">
          <button @click="sidebarOpen = !sidebarOpen" class="md:hidden p-2 rounded-md text-gray-500 hover:bg-gray-100">
            <MenuIcon class="w-6 h-6" />
          </button>
          <div class="flex items-center gap-2">
            <div class="w-8 h-8 rounded-full bg-gradient-to-br from-indigo-900 to-purple-800 flex items-center justify-center text-white">
              <ServerIcon class="w-4 h-4" />
            </div>
            <span class="text-xl font-bold text-gray-800">SaveMyData</span>
          </div>
        </div>

        <div class="flex items-center gap-4">
          <button class="p-2 rounded-full text-gray-500 hover:bg-gray-100">
            <BellIcon class="w-5 h-5" />
          </button>
          <div class="relative">
            <button @click="profileOpen = !profileOpen" class="flex items-center gap-2">
              <div class="w-8 h-8 rounded-full bg-pink-600 flex items-center justify-center text-white font-medium">
                {{ userInitials }}
              </div>
              <span class="hidden md:block text-sm font-medium text-gray-700">{{ user.name }}</span>
              <ChevronDownIcon class="w-4 h-4 text-gray-500" />
            </button>

            <!-- Menu profil -->
            <div v-if="profileOpen" class="absolute right-0 mt-2 w-48 bg-white rounded-md shadow-lg py-1 z-10 border border-gray-200">
              <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100">Profil</a>
              <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100">Paramètres</a>
              <div class="border-t border-gray-200 my-1"></div>
              <a href="#" @click.prevent="logout" class="block px-4 py-2 text-sm text-red-600 hover:bg-gray-100">Déconnexion</a>
            </div>
          </div>
        </div>
      </div>
    </header>

    <div class="flex flex-1 overflow-hidden">
      <!-- Barre latérale -->
      <aside :class="[
        'bg-white border-r border-gray-200 w-64 flex-shrink-0 flex flex-col transition-all duration-300 ease-in-out',
        sidebarOpen ? 'translate-x-0' : '-translate-x-full md:translate-x-0'
      ]">
        <div class="p-4">
          <div class="relative">
            <SearchIcon class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 w-4 h-4" />
            <input
                type="text"
                placeholder="Rechercher..."
                class="w-full pl-10 pr-4 py-2 rounded-md border border-gray-200 text-sm focus:outline-none focus:ring-2 focus:ring-pink-500/20 focus:border-pink-500"
            />
          </div>
        </div>

        <nav class="flex-1 px-2 py-4 space-y-1">
          <a href="#" class="flex items-center gap-3 px-3 py-2 text-sm font-medium rounded-md bg-pink-50 text-pink-700">
            <LayoutDashboardIcon class="w-5 h-5" />
            Tableau de bord
          </a>
          <a href="#" class="flex items-center gap-3 px-3 py-2 text-sm font-medium rounded-md text-gray-700 hover:bg-gray-50">
            <FileTextIcon class="w-5 h-5" />
            Documents
          </a>
          <a href="#" class="flex items-center gap-3 px-3 py-2 text-sm font-medium rounded-md text-gray-700 hover:bg-gray-50">
            <FolderIcon class="w-5 h-5" />
            Dossiers
          </a>
          <a href="#" class="flex items-center gap-3 px-3 py-2 text-sm font-medium rounded-md text-gray-700 hover:bg-gray-50">
            <ShieldIcon class="w-5 h-5" />
            Sécurité
          </a>
          <a href="#" class="flex items-center gap-3 px-3 py-2 text-sm font-medium rounded-md text-gray-700 hover:bg-gray-50">
            <UsersIcon class="w-5 h-5" />
            Partage
          </a>
          <a href="#" class="flex items-center gap-3 px-3 py-2 text-sm font-medium rounded-md text-gray-700 hover:bg-gray-50">
            <SettingsIcon class="w-5 h-5" />
            Paramètres
          </a>
        </nav>

        <div class="p-4 border-t border-gray-200">
          <div class="bg-gray-50 rounded-lg p-3">
            <div class="flex items-center gap-3 mb-2">
              <HardDriveIcon class="w-5 h-5 text-gray-500" />
              <span class="text-sm font-medium text-gray-700">Stockage</span>
            </div>
            <div class="w-full bg-gray-200 rounded-full h-2.5">
              <div class="bg-pink-600 h-2.5 rounded-full" style="width: 45%"></div>
            </div>
            <div class="flex justify-between mt-2 text-xs text-gray-500">
              <span>4.5 GB utilisés</span>
              <span>10 GB total</span>
            </div>
          </div>
        </div>
      </aside>

      <!-- Contenu principal -->
      <main class="flex-1 overflow-auto p-6">
        <div class="max-w-7xl mx-auto">
          <h1 class="text-2xl font-bold text-gray-800 mb-6">Tableau de bord</h1>

          <!-- Statistiques -->
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
            <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6">
              <div class="flex items-center justify-between mb-4">
                <h3 class="text-sm font-medium text-gray-500">Documents</h3>
                <div class="p-2 rounded-lg bg-blue-50">
                  <FileTextIcon class="w-5 h-5 text-blue-500" />
                </div>
              </div>
              <p class="text-3xl font-bold text-gray-800">128</p>
              <p class="text-sm text-gray-500 mt-1">
                <span class="text-green-500 font-medium">+12%</span> depuis le mois dernier
              </p>
            </div>

            <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6">
              <div class="flex items-center justify-between mb-4">
                <h3 class="text-sm font-medium text-gray-500">Dossiers</h3>
                <div class="p-2 rounded-lg bg-purple-50">
                  <FolderIcon class="w-5 h-5 text-purple-500" />
                </div>
              </div>
              <p class="text-3xl font-bold text-gray-800">24</p>
              <p class="text-sm text-gray-500 mt-1">
                <span class="text-green-500 font-medium">+5%</span> depuis le mois dernier
              </p>
            </div>

            <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6">
              <div class="flex items-center justify-between mb-4">
                <h3 class="text-sm font-medium text-gray-500">Partages</h3>
                <div class="p-2 rounded-lg bg-green-50">
                  <UsersIcon class="w-5 h-5 text-green-500" />
                </div>
              </div>
              <p class="text-3xl font-bold text-gray-800">36</p>
              <p class="text-sm text-gray-500 mt-1">
                <span class="text-red-500 font-medium">-2%</span> depuis le mois dernier
              </p>
            </div>

            <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6">
              <div class="flex items-center justify-between mb-4">
                <h3 class="text-sm font-medium text-gray-500">Stockage</h3>
                <div class="p-2 rounded-lg bg-pink-50">
                  <HardDriveIcon class="w-5 h-5 text-pink-500" />
                </div>
              </div>
              <p class="text-3xl font-bold text-gray-800">45%</p>
              <p class="text-sm text-gray-500 mt-1">
                <span class="text-green-500 font-medium">4.5 GB</span> sur 10 GB
              </p>
            </div>
          </div>

          <!-- Documents récents -->
          <div class="bg-white rounded-xl shadow-sm border border-gray-200 mb-8">
            <div class="px-6 py-4 border-b border-gray-200">
              <h2 class="text-lg font-medium text-gray-800">Documents récents</h2>
            </div>
            <div class="overflow-x-auto">
              <table class="min-w-full divide-y divide-gray-200">
                <thead class="bg-gray-50">
                <tr>
                  <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Nom</th>
                  <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Type</th>
                  <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Taille</th>
                  <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Modifié</th>
                  <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Actions</th>
                </tr>
                </thead>
                <tbody class="bg-white divide-y divide-gray-200">
                <tr v-for="(doc, index) in recentDocuments" :key="index">
                  <td class="px-6 py-4 whitespace-nowrap">
                    <div class="flex items-center">
                      <component :is="getDocumentIcon(doc.type)" class="w-5 h-5 text-gray-500 mr-3" />
                      <span class="text-sm font-medium text-gray-900">{{ doc.name }}</span>
                    </div>
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">{{ doc.type }}</td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">{{ doc.size }}</td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">{{ doc.modified }}</td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                    <div class="flex items-center gap-2">
                      <button class="p-1 rounded-md hover:bg-gray-100">
                        <EyeIcon class="w-4 h-4 text-gray-500" />
                      </button>
                      <button class="p-1 rounded-md hover:bg-gray-100">
                        <DownloadIcon class="w-4 h-4 text-gray-500" />
                      </button>
                      <button class="p-1 rounded-md hover:bg-gray-100">
                        <MoreVerticalIcon class="w-4 h-4 text-gray-500" />
                      </button>
                    </div>
                  </td>
                </tr>
                </tbody>
              </table>
            </div>
            <div class="px-6 py-3 border-t border-gray-200 bg-gray-50">
              <a href="#" class="text-sm font-medium text-pink-600 hover:text-pink-700">Voir tous les documents →</a>
            </div>
          </div>

          <!-- Activité récente -->
          <div class="bg-white rounded-xl shadow-sm border border-gray-200">
            <div class="px-6 py-4 border-b border-gray-200">
              <h2 class="text-lg font-medium text-gray-800">Activité récente</h2>
            </div>
            <div class="p-6">
              <div class="flow-root">
                <ul class="-mb-8">
                  <li v-for="(activity, index) in recentActivities" :key="index">
                    <div class="relative pb-8">
                      <span v-if="index !== recentActivities.length - 1" class="absolute top-5 left-5 -ml-px h-full w-0.5 bg-gray-200" aria-hidden="true"></span>
                      <div class="relative flex items-start space-x-3">
                        <div class="relative">
                          <div :class="[
                            'h-10 w-10 rounded-full flex items-center justify-center ring-8 ring-white',
                            getActivityColor(activity.type)
                          ]">
                            <component :is="getActivityIcon(activity.type)" class="w-5 h-5 text-white" />
                          </div>
                        </div>
                        <div class="min-w-0 flex-1">
                          <div>
                            <div class="text-sm font-medium text-gray-900">
                              {{ activity.user }}
                            </div>
                            <p class="mt-0.5 text-sm text-gray-500">
                              {{ activity.action }}
                            </p>
                          </div>
                          <div class="mt-2 text-sm text-gray-700">
                            <p>{{ activity.description }}</p>
                          </div>
                        </div>
                        <div class="text-right text-sm whitespace-nowrap text-gray-500">
                          <time>{{ activity.time }}</time>
                        </div>
                      </div>
                    </div>
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import {
  ServerIcon, MenuIcon, BellIcon, ChevronDownIcon, SearchIcon,
  LayoutDashboardIcon, FileTextIcon, FolderIcon, ShieldIcon,
  UsersIcon, SettingsIcon, HardDriveIcon, EyeIcon, DownloadIcon,
  MoreVerticalIcon, FileIcon, ImageIcon, FileSpreadsheetIcon,
  UploadIcon, EditIcon, TrashIcon, ShareIcon
} from 'lucide-vue-next'

const sidebarOpen = ref(false)
const profileOpen = ref(false)

// Données utilisateur
const user = {
  name: 'Jean Dupont',
  email: 'jean.dupont@example.com'
}

// Calcul des initiales de l'utilisateur
const userInitials = computed(() => {
  return user.name
      .split(' ')
      .map(name => name[0])
      .join('')
      .toUpperCase()
})

// Documents récents
const recentDocuments = [
  { name: 'Carte d\'identité.pdf', type: 'PDF', size: '2.4 MB', modified: 'Il y a 2 heures' },
  { name: 'Facture EDF Janvier.pdf', type: 'PDF', size: '1.2 MB', modified: 'Il y a 1 jour' },
  { name: 'Passeport.jpg', type: 'Image', size: '3.8 MB', modified: 'Il y a 3 jours' },
  { name: 'Relevé bancaire.xlsx', type: 'Spreadsheet', size: '0.8 MB', modified: 'Il y a 1 semaine' },
  { name: 'Contrat de travail.pdf', type: 'PDF', size: '4.2 MB', modified: 'Il y a 2 semaines' }
]

// Activités récentes
const recentActivities = [
  {
    user: 'Vous',
    action: 'Téléchargement',
    description: 'Vous avez téléchargé Carte d\'identité.pdf',
    time: 'Il y a 2 heures',
    type: 'download'
  },
  {
    user: 'Système',
    action: 'Sauvegarde',
    description: 'Sauvegarde automatique effectuée',
    time: 'Il y a 6 heures',
    type: 'backup'
  },
  {
    user: 'Vous',
    action: 'Téléversement',
    description: 'Vous avez ajouté Facture EDF Janvier.pdf',
    time: 'Il y a 1 jour',
    type: 'upload'
  },
  {
    user: 'Vous',
    action: 'Modification',
    description: 'Vous avez renommé un dossier en "Documents importants"',
    time: 'Il y a 3 jours',
    type: 'edit'
  }
]

// Fonctions utilitaires
const getDocumentIcon = (type) => {
  switch (type) {
    case 'PDF': return FileTextIcon
    case 'Image': return ImageIcon
    case 'Spreadsheet': return FileSpreadsheetIcon
    default: return FileIcon
  }
}

const getActivityIcon = (type) => {
  switch (type) {
    case 'upload': return UploadIcon
    case 'download': return DownloadIcon
    case 'edit': return EditIcon
    case 'delete': return TrashIcon
    case 'share': return ShareIcon
    case 'backup': return HardDriveIcon
    default: return FileIcon
  }
}

const getActivityColor = (type) => {
  switch (type) {
    case 'upload': return 'bg-green-500'
    case 'download': return 'bg-blue-500'
    case 'edit': return 'bg-yellow-500'
    case 'delete': return 'bg-red-500'
    case 'share': return 'bg-purple-500'
    case 'backup': return 'bg-gray-500'
    default: return 'bg-gray-500'
  }
}

// Fonction de déconnexion
const logout = () => {
  console.log('Déconnexion')

  // Émettre un événement pour informer le parent de la déconnexion
  emit('logout')
}

// Définir les événements pour communiquer avec le composant parent
const emit = defineEmits(['logout'])
</script>