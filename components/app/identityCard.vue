<script setup>
const HORSE_NAME = 'Mustang'
const HORSE_OWNER = 'Hugo'
</script>

<template>
    <div class="flex flex-col gap-6">
        <Card class="overflow-hidden">
            <CardContent class="grid h-[80vh] p-0 md:grid-cols-2">
                <div class="relative block min-h-48 bg-muted">
                    <img
                        src="https://thumbs.dreamstime.com/b/horse-head-5971041.jpg"
                        alt="Image"
                        class="absolute inset-0 h-full w-full object-cover dark:brightness-[0.2] dark:grayscale"
                    />
                </div>
                <form class="overflow-y-scroll p-6 md:p-8">
                    <div class="flex flex-col gap-6">
                        <div class="flex flex-col items-center text-center">
                            <h1 class="text-2xl font-bold">{{ HORSE_NAME }}</h1>
                            <p class="text-balance text-muted-foreground">
                                Owned by {{ HORSE_OWNER }}
                            </p>
                        </div>
                        <div class="grid gap-2">
                            <!-- FEI ID -->

                            <Label for="feiId">FEI ID</Label>
                            <Input
                                id="feiId"
                                disabled
                                type="text"
                                value="106EO39"
                            />
                        </div>
                        <div class="grid gap-2">
                            <!-- STUD BOOK -->
                            <Label for="studBook">Stud Book</Label>
                            <Input
                                id="studBook"
                                disabled
                                type="text"
                                value="KWPN"
                            />
                        </div>
                        <div class="grid gap-2">
                            <!-- REGISTRATION -->
                            <Label for="registration">Registration</Label>
                            <Input
                                id="registration"
                                disabled
                                type="text"
                                value="A18"
                            />
                        </div>
                        <div class="grid gap-2">
                            <!-- SEX -->
                            <Label for="registration">Sex</Label>
                            <Input
                                id="registration"
                                disabled
                                type="text"
                                value="Stallion"
                            />
                        </div>
                        <div class="grid gap-2">
                            <!-- DATE OF BIRTH -->
                            <Label for="registration">Date of birth</Label>
                            <Input
                                id="registration"
                                disabled
                                type="date"
                                value="2013-03-13"
                            />
                        </div>
                    </div>
                </form>
            </CardContent>
        </Card>
    </div>
</template>
