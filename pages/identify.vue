<script setup>
const isLoading = ref(false)

onMounted(() => {
    setTimeout(() => {
        isLoading.value = false
    }, 5000)
})
</script>

<template>
    <main
        class="flex h-screen w-screen flex-col items-center justify-center gap-12 px-5 py-10"
    >
        <div class="h-full w-full max-w-screen-sm bg-slate-200">
            <template v-if="isLoading">
                <div>loading...</div>
            </template>
            <template v-else>
                <div>identify</div>
            </template>
        </div>
    </main>
</template>

<style scoped></style>
