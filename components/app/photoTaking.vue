<script setup>
import { Progress } from '@/components/ui/progress'

const REQUIRED_PICTURES = 4

const facingMode = ref('environment')
const camera = useTemplateRef('camera')
const cameras = ref([])
const pictures = ref([])
const isLoading = ref(true)
const progress = computed(
    () => (pictures.value.length / REQUIRED_PICTURES) * 100
)

const picturesDisplay = computed(() => {
    if (pictures.value.length >= REQUIRED_PICTURES) return pictures.value

    return pictures.value.concat(
        Array(REQUIRED_PICTURES - pictures.value.length).fill(null)
    )
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

const removePicture = (index) => pictures.value.splice(index, 1)

onMounted(async () => {
    const devices = await camera.value?.devices()
    cameras.value = devices.filter((device) => device.kind === 'videoinput')
})
</script>

<template>
    <div class="mb-4 w-full">
        <div class="flex flex-row justify-between">
            <TypoP
                >Take {{ REQUIRED_PICTURES }} pictures on different
                angles.</TypoP
            >
            <TypoMuted>{{ pictures.length }}/{{ REQUIRED_PICTURES }}</TypoMuted>
        </div>
        <Progress v-model="progress" />
    </div>
    <BaseCamera
        v-if="pictures.length < REQUIRED_PICTURES"
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
            <Button size="lg" @click="takePicture()">
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
        <div
            v-for="(picture, index) in picturesDisplay"
            :key="picture"
            class="relative w-1/3"
        >
            <img :src="picture" />
            <template v-if="picture">
                <Button
                    size="xs"
                    variant="destructive"
                    class="absolute right-1 top-1 z-10"
                    @click="removePicture(index)"
                    >X</Button
                >
            </template>
        </div>
    </div>

    <div
        v-if="pictures.length === REQUIRED_PICTURES"
        class="mt-6 flex justify-center"
    >
        <NuxtLink to="/identify">
            <Button>Identify</Button>
        </NuxtLink>
    </div>
</template>

<style scoped></style>
