<script setup>
import { Progress } from '@/components/ui/progress'

const facingMode = ref('environment')
const camera = useTemplateRef('camera')
const cameras = ref([])
const pictures = ref([])
const isLoading = ref(true)
const progress = computed(() => (pictures.value.length / 3) * 100)

const picturesDisplay = computed(() => {
    if (pictures.value.length >= 3) return pictures.value

    return pictures.value.concat(Array(3 - pictures.value.length).fill(null))
})

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
    <div class="mb-4 w-full">
        <div class="flex flex-row justify-between">
            <TypoP>Take 3 pictures on diffrent angles.</TypoP>
            <TypoMutted>{{ pictures.length }}/3</TypoMutted>
        </div>
        <Progress v-model="progress" />
    </div>
    <BaseCamera
        v-if="pictures.length < 3"
        ref="camera"
        :resolution="{ width: 1500, height: 2000 }"
        :facing-mode="cameras.length > 1 ? facingMode : 'environment'"
        autoplay
        :playsinline="true"
        @loading="isLoading = true"
        @started="isLoading = false"
    >
        <div
            v-show="!isLoading"
            class="absolute bottom-5 left-1/2 -translate-x-1/2 transform"
        >
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
    <div class="mt-6 flex flex-row gap-2">
        <div v-for="picture in picturesDisplay" :key="picture" class="w-1/3">
            <img :src="picture" />
        </div>
    </div>

    <div class="mt-6 flex justify-center">
        <Button>Identify</Button>
    </div>
</template>

<style scoped></style>
