<template>
  <div class="min-h-screen bg-gray-50 font-inter p-4 overflow-y-auto">
    <div class="w-full mx-auto bg-white rounded-lg shadow-sm p-6">
      <!-- En-tête -->
      <div class="flex items-center justify-between mb-6">
        <!-- Partie gauche avec le stepper -->
        <div class="flex items-center gap-6">
          <!-- Présentez-vous -->
          <div class="flex items-center">
            <img src="./assets/icons/user.svg" alt="user" class="w-5 h-5">
            <span class="text-sm text-left mx-2 font-bold">Présentez-vous</span>
            <img src="./assets/icons/arrow-step.svg" alt="arrow" class="w-6 h-6">
          </div>

          <!-- Autres contributions -->
          <div class="flex items-center">
            <img src="./assets/icons/mark-pen.svg" alt="mark-pen" class="w-5 h-5">
            <span class="text-sm text-left mx-2">Autres contributions</span>
            <img src="./assets/icons/arrow-step.svg" alt="arrow" class="w-6 h-6">
          </div>

          <!-- Contributions -->
          <div class="flex items-center">
            <img src="./assets/icons/briefcase.svg" alt="briefcase" class="w-5 h-5">
            <span class="text-sm text-left mx-2">Contributions</span>
          </div>
        </div>

        <!-- Partie droite avec les boutons -->
        <div class="flex items-center ml-20">
          <button class="flex items-center gap-2 border-none text-sm font-medium bg-transparent">
            <img src="./assets/icons/Vector.png" alt="listen" class="w-5 h-5">
            Écouter
          </button>
          <button class="flex items-center gap-2 text-sm font-medium bg-[#F4F4F5] text-black px-4 py-2 rounded-md">
            <img src="./assets/icons/phone.svg" alt="phone" class="w-5 h-5">
            N°Vert
          </button>
        </div>
      </div>

      <!-- Temps de remplissage -->
      <div class="mb-6">
        <h2 class="text-lg font-medium mb-1 text-left">Temps de remplissage :</h2>
        <p class="text-sm text-gray-500 text-left">5 minutes</p>
      </div>

      <!-- Formulaire -->
      <form @submit.prevent="submitForm">
        <!-- Question anonymat -->
        <div class="mb-6">
          <p class="mb-3 text-left">Souhaitez-vous soumettre votre contribution dans l'anonymat ?</p>
          <div class="flex gap-4">
            <label class="relative flex-1">
              <input type="radio" name="anonymat" value="oui" class="peer hidden">
              <div class="border rounded-lg p-6 h-24 cursor-pointer peer-checked:border-black peer-checked:border-2 relative">
                <div class="absolute top-4 right-4 w-4 h-4 rounded-full border border-gray-300 peer-checked:bg-black">
                  <img 
                    src="./assets/icons/cocher.svg" 
                    alt="coché" 
                    class="absolute inset-0 w-4 h-4 opacity-0 peer-checked:opacity-100"
                  >
                </div>
                <div class="flex flex-col">
                  <span class="text-left font-medium">Oui</span>
                  <span class="text-sm text-gray-500 text-left">Utilisation des données<br>récupérées.</span>
                </div>
              </div>
            </label>

            <label class="relative flex-1">
              <input type="radio" name="anonymat" value="non" class="peer hidden">
              <div class="border rounded-lg p-6 h-24 cursor-pointer peer-checked:border-black peer-checked:border-2 relative">
                <div class="absolute top-4 right-4 w-4 h-4 rounded-full border border-gray-300 peer-checked:bg-black">
                  <img 
                    src="./assets/icons/cocher.svg" 
                    alt="coché" 
                    class="absolute inset-0 w-4 h-4 opacity-0 peer-checked:opacity-100"
                  >
                </div>
                <div class="flex flex-col">
                  <span class="text-left font-medium">Non</span>
                  <span class="text-sm text-gray-500 text-left">Utilisation des données<br>récupérées.</span>
                </div>
              </div>
            </label>
          </div>
        </div>

        <!-- Informations personnelles -->
        <div class="grid grid-cols-2 gap-6">
          <div class="form-group">
            <label class="block mb-1 text-left">Prénom <span class="text-red-500">*</span></label>
            <input type="text" class="w-full border rounded-md p-2 text-left" placeholder="Saisir votre prénom">
          </div>
          <div class="form-group">
            <label class="block mb-1 text-left">Nom <span class="text-red-500">*</span></label>
            <input type="text" class="w-full border rounded-md p-2 text-left" placeholder="Saisir votre nom">
          </div>
        </div>

        <div class="form-group mt-4">
          <label class="block mb-1 text-left">Téléphone <span class="text-red-500">*</span></label>
          <input type="tel" class="w-full border rounded-md p-2 text-left" placeholder="+237">
          <p class="text-sm text-gray-500 mt-1 text-left">Ex: +237 6 XXXX XXXX (numéro téléphone)</p>
        </div>

        <div class="form-group mt-4">
          <label class="block mb-1 text-left">Email <span class="text-red-500">*</span></label>
          <input type="email" class="w-full border rounded-md p-2 text-left" placeholder="Saisir votre adresse email">
        </div>

        <div class="grid grid-cols-2 gap-6 mt-4">
          <div class="form-group">
            <label class="block mb-1 text-left">Age <span class="text-red-500">*</span></label>
            <select class="w-full border rounded-md p-2 text-left">
              <option value="">Choisissez votre tranche d'âge</option>
            </select>
          </div>
          <div class="form-group">
            <label class="block mb-1 text-left">Sexe <span class="text-red-500">*</span></label>
            <select class="w-full border rounded-md p-2 text-left">
              <option value="">Choisissez votre sexe</option>
            </select>
          </div>
        </div>

        <div class="mt-4">
          <p class="mb-2 text-left">Résidez-vous au Cameroun ? <span class="text-red-500">*</span></p>
          <div class="flex gap-8">
            <label class="flex items-center gap-2">
              <input type="radio" name="residence" value="oui">
              <span class="text-left">Oui</span>
            </label>
            <label class="flex items-center gap-2">
              <input type="radio" name="residence" value="non">
              <span class="text-left">Non</span>
            </label>
          </div>
        </div>

        <div class="form-group mt-4">
          <label class="block mb-1 text-left">Nationalité <span class="text-red-500">*</span></label>
          <input type="text" class="w-full border rounded-md p-2 text-left" placeholder="Saisir votre nationalité">
        </div>

        <div class="grid grid-cols-2 gap-6 mt-4">
          <div class="form-group">
            <label class="block mb-1 text-left">Département <span class="text-red-500">*</span></label>
            <select class="w-full border rounded-md p-2 text-left">
              <option value="">Choisissez votre département</option>
            </select>
          </div>
          <div class="form-group">
            <label class="block mb-1 text-left">Commune <span class="text-red-500">*</span></label>
            <select class="w-full border rounded-md p-2 text-left">
              <option value="">Choisissez votre commune</option>
            </select>
          </div>
        </div>

        <div class="form-group mt-4">
          <label class="block mb-1 text-left">Profession <span class="text-red-500">*</span></label>
          <input type="text" class="w-full border rounded-md p-2 text-left" placeholder="Choisissez votre profession">
        </div>

        <button type="submit" class="mt-6 mb-4 bg-black text-white px-6 py-2 rounded-md">
          Suivant
        </button>
      </form>
    </div>
  </div>
</template>

<script setup>
const submitForm = () => {
  // Logique de soumission du formulaire
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&display=swap');

.font-inter {
  font-family: 'Inter', sans-serif;
}

/* Ajout des styles pour l'animation de la coche */
input[type="radio"]:checked + div .w-4 img {
  opacity: 1;
}
</style>
