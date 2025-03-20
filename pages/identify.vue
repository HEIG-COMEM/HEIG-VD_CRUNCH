<script setup>
const isLoading = ref(true)

onMounted(() => {
    setTimeout(() => {
        isLoading.value = false
    }, 2500)
})
</script>

<template>
    <main
        class="flex h-screen w-screen flex-col items-center justify-center gap-12 px-5 py-10"
    >
        <div class="h-full w-full max-w-screen-sm">
            <template v-if="isLoading">
                <div
                    class="flex h-full w-full flex-col items-center justify-center"
                >
                    <AppLoading />
                    <TypoLead>Loading...</TypoLead>
                </div>
            </template>
            <template v-else>
                <AppIdentityCard />
            </template>
        </div>
    </main>
</template>

<style scoped></style>
