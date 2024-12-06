<script setup>
import { ref } from 'vue'
import Loading from './components/Loading.vue'

const base_url = 'https://parseapi.back4app.com/classes/Dataset_Cell_Phones_Model_Brand?limit=10&keys=Brand,Model,Announced,Battery,Colors,Dimensions,Internal_memory,RAM'

const misApis = {
    'X-Parse-Application-Id': 'MEqvn3N742oOXsF33z6BFeezRkW8zXXh4nIwOQUT',
    'X-Parse-Master-Key': 'uZ1r1iHnOQr5K4WggIibVczBZSPpWfYbSRpD6INw'
}

const isLoading = ref(true)
const phoneList = ref([])

const getPhones = async () => {

    try {

        isLoading.value = true
        const response = await fetch(base_url, { headers: misApis })
        const data = await response.json()
        phoneList.value = data.results.map((phone) => ({
            id: phone.objectId,
            brand: phone.Brand,
            model: phone.Model,
            announced: phone.Announced,
            battery: phone.Battery,
            colors: phone.Colors,
            ram: phone.RAM,
            internal_memory: phone.internal_memory
        }))
        isLoading.value = false
    } catch (error) {
        console.error('Error al obtener los teléfonos:', error)
    }
}

getPhones()
</script>

<template>
    <Loading v-if="isLoading" />
    <div v-else>
        <h3 style="color: #ADD8E6;">Lista de Teléfonos Antiguos</h3>
        <template v-for="phone in phoneList" :key="phone.id">
            <RouterLink :to="`/phone/${phone.id}`"> {{ phone.brand }} - {{ phone.model }} </RouterLink> <br />
        </template>
    </div>
</template>
