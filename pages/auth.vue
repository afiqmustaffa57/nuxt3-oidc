<template>
	<h3>Authenticating...</h3>
</template>

<script lang="ts" setup>
import { useServices } from '@/composables/useServices'

const services = useServices()
const router = useRouter()

const authenticateOidc = async () => {
	try {
		const resp = await services.$auth.signInCallback()
		console.log('resp', resp)
		const redirectUrl = services.$webStorage.getItem('oidc_requested_url')
		router.push(redirectUrl)
	} catch (error) {
		console.log(error)
	}
}

await authenticateOidc()
console.log('auth page')
</script>
