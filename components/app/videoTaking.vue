<script setup lang="ts">
import { Alert, AlertDescription, AlertTitle } from '@/components/ui/alert'
import { AlertCircle } from 'lucide-vue-next'
</script>

<template>
    <Alert variant="destructive">
        <AlertCircle class="h-4 w-4" />
        <AlertTitle>Work in progress</AlertTitle>
        <AlertDescription>
            This feature is not yet available. Please check back later.
        </AlertDescription>
    </Alert>
</template>
