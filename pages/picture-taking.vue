<script setup>
import { Tabs, TabsContent, TabsList, TabsTrigger } from '@/components/ui/tabs'

const speed = ref(-Infinity)

const isSpeedGood = computed(() => speed.value >= 5)
const isConnectionLost = computed(() => speed.value <= 0)

const updateSpeed = () => {
    const connection =
        navigator.connection ||
        navigator.mozConnection ||
        navigator.webkitConnection
    console.log(connection)
    if (connection) {
        speed.value = connection.downlink
    } else {
        speed.value = -Infinity
    }
}

onMounted(() => {
    updateSpeed()
    navigator.connection.addEventListener('change', updateSpeed)
})
</script>

<template>
    <main
        class="flex h-screen w-screen flex-col items-center justify-center gap-12 px-5 py-10"
    >
        <div class="flex flex-col items-center justify-center gap-1">
            <BaseH1>EQUiD</BaseH1>
            <template v-if="isConnectionLost">
                <BaseLead
                    >We are unable to determine your internet speed, please
                    check your connection</BaseLead
                >
            </template>
            <template v-else>
                <template v-if="isSpeedGood">
                    <BaseLead class="text-center"
                        >Based on your internet speed you can either use the
                        video or image scanning method</BaseLead
                    >
                </template>
                <template v-else>
                    <BaseLead
                        >Based on your internet speed you can only use the image
                        scaning</BaseLead
                    >
                </template>
            </template>
        </div>
        <section class="h-full w-full max-w-screen-sm bg-slate-400">
            <Tabs v-if="!isConnectionLost" default-value="photo" class="w-full">
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
            <template v-else>
                <BaseMuted>
                    Please check your connection and try again
                </BaseMuted>
            </template>
        </section>
    </main>
</template>

<style scoped></style>
