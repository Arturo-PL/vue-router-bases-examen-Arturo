<script setup>
import { RouterLink, useRoute } from 'vue-router'
import { ref } from 'vue'

const base_url = 'https://parseapi.back4app.com/classes/Dataset_Cell_Phones_Model_Brand'

const misApis = {
    'X-Parse-Application-Id': 'MEqvn3N742oOXsF33z6BFeezRkW8zXXh4nIwOQUT',
    'X-Parse-Master-Key': 'uZ1r1iHnOQr5K4WggIibVczBZSPpWfYbSRpD6INw'
}

const route = useRoute()
const { id } = route.params
const phone = ref({})
const isLoading = ref(true)

// Función para obtener detalles de un teléfono
const getPhoneDetails = async () => {
    
    try {
        const response = await fetch(`${base_url}/${id}`, { headers: misApis })
        const data = await response.json()
        phone.value = data
        isLoading.value = false
    } catch (error) {
        console.error('Error al obtener detalles del teléfono:', error)
    }
}

getPhoneDetails()
</script>

<template>
    <div class="d-flex justify-content-center align-items-center vh-100">
        <Loading v-if="isLoading" />
        <div v-else class="card" style="width: 18rem;">
            <div class="card-body">
                <h5 class="card-title">{{ phone.Brand }} - {{ phone.Model }}</h5>
                <p class="card-text"><strong>Anunciado:</strong> {{ phone.Announced }}</p>
                <p class="card-text"><strong>Batería:</strong> {{ phone.Battery }}</p>
                <p class="card-text"><strong>Colores:</strong> {{ phone.Colors }}</p>
                <p class="card-text"><strong>RAM:</strong> {{ phone.RAM }}</p>
                <p class="card-text"><strong>Almacenamiento Interno:</strong> {{ phone.Internal_memory }}</p>
                <RouterLink class="btn btn-success" to="/phone">Regresar</RouterLink>
            </div>
        </div>
    </div>
</template>

