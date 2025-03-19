<script setup>
const facingMode = ref('environment')
const camera = useTemplateRef('camera')
const cameras = ref([])
const pictures = ref([])
const isLoading = ref(false)

const takePicture = async () => {
    const blob = await camera.value.snapshot()
    const base64 = await new Promise((resolve) => {
        const reader = new FileReader()
        reader.readAsDataURL(blob)
        reader.onloadend = () => {
            resolve(reader.result)
        }
    })
    pictures.value.push(base64)
}

onMounted(async () => {
    const devices = await camera.value?.devices()
    cameras.value = devices.filter((device) => device.kind === 'videoinput')
})
</script>

<template>
    <p v-if="isLoading">Load</p>
    <TypoP>Lorem</TypoP>
    <BaseCamera
        ref="camera"
        :resolution="{ width: 1500, height: 2000 }"
        :facing-mode="cameras.length > 1 ? facingMode : 'environment'"
        autoplay
        :playsinline="true"
        @loading="isLoading = true"
        @started="isLoading = false"
    >
        <div class="absolute bottom-5 left-1/2 -translate-x-1/2 transform">
            <Button size="icon" @click="takePicture()">
                <svg
                    width="60"
                    height="60"
                    viewBox="0 0 60 60"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                >
                    <circle cx="30" cy="30" r="29.5" stroke="white" />
                    <circle cx="30" cy="30" r="20" fill="white" />
                </svg>
            </Button>
        </div>
    </BaseCamera>
</template>

<style scoped></style>
