<script setup>
import { Tabs, TabsContent, TabsList, TabsTrigger } from '@/components/ui/tabs'

const speed = ref(-Infinity)

const isSpeedGood = computed(() => speed.value >= 2)
const isConnectionLost = computed(() => speed.value <= 0)
const connectionNotSupported = computed(() => speed.value === -Infinity)

const updateSpeed = () => {
    const connection =
        navigator.connection ||
        navigator.mozConnection ||
        navigator.webkitConnection
    if (connection) {
        speed.value = connection.downlink
    } else {
        speed.value = -Infinity
    }
}

onMounted(() => {
    updateSpeed()
    navigator?.connection?.addEventListener('change', updateSpeed)
})
</script>

<template>
    <main
        class="flex h-screen w-screen flex-col items-center justify-center gap-12 px-5 py-10"
    >
        <div class="flex flex-col items-center justify-center gap-1">
            <TypoH1>EQUiD</TypoH1>
            <TypoLead class="text-center">
                <template v-if="connectionNotSupported">
                    Based on your internet speed you can either use the video or
                    image scanning method
                </template>
                <template v-else-if="isConnectionLost">
                    We are unable to determine your internet speed, please check
                    your connection
                </template>
                <template v-else-if="isSpeedGood">
                    Based on your internet speed you can either use the video or
                    image scanning method
                </template>
                <template v-else>
                    Based on your internet speed you can only use the image
                    scanning
                </template>
            </TypoLead>
        </div>
        <section class="h-full w-full max-w-screen-sm bg-slate-400">
            <template v-if="connectionNotSupported || isSpeedGood">
                <Tabs default-value="photo" class="w-full">
                    <TabsList>
                        <TabsTrigger value="photo">Pictures</TabsTrigger>
                        <TabsTrigger value="video">Video</TabsTrigger>
                    </TabsList>
                    <TabsContent value="photo">
                        <AppPhotoTaking />
                    </TabsContent>
                    <TabsContent value="video">
                        <AppVideoTaking />
                    </TabsContent>
                </Tabs>
            </template>
            <template v-else-if="isConnectionLost">
                <TypoMuted>
                    Please check your connection and try again
                </TypoMuted>
            </template>
            <template v-else>
                <AppPhotoTaking />
            </template>
        </section>
    </main>
</template>

<style scoped></style>
