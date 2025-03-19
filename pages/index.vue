<template>
    <main class="w-sceen relative h-screen">
        <div
            class="absolute left-1/2 top-1/2 z-10 flex -translate-x-1/2 -translate-y-1/2 transform flex-col items-center justify-center gap-12"
        >
            <BaseH1>EQUiD</BaseH1>
            <NuxtLink
                to="/picture-taking"
                class="group rounded-full border border-black/5 bg-neutral-200/50 text-base text-white transition-all ease-in hover:cursor-pointer hover:bg-neutral-200 dark:border-white/5 dark:bg-neutral-900 dark:hover:bg-neutral-800"
            >
                <StunningShimmerText
                    :shimmer-width="40"
                    class="inline-flex items-center justify-center px-4 py-1 text-neutral-700 transition ease-out hover:text-neutral-600 hover:duration-300 hover:dark:text-neutral-400"
                    >✨ Proof of Concept</StunningShimmerText
                >
            </NuxtLink>
        </div>
        <StunningGodRay />
    </main>
</template>
