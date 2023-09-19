<template>
	<h3>Deslogando...</h3>
</template>

<script lang="ts" setup>
import { useServices } from '@/composables/useServices'
import { useAuth } from '~~/stores/auth'

const services = useServices()
const authStore = useAuth()

const logOutOidc = async () => {
	try {
		let user = await services.$auth.getUser();
		console.log('user', user)
		authStore.clearUserSession()
		services.$webStorage.clearStorage()
		await services.$auth.logout(user?.id_token!)
	} catch (error) {
		console.log(error)
	}
}

await logOutOidc()
</script>
