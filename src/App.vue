<script lang="ts">
import {fakerEN} from '@faker-js/faker'
import {defineComponent} from 'vue'

export default defineComponent({
    data() {
        return {
            username: '',
        }
    },
    methods: {
        generateRandomUserName() {
            return `${fakerEN.word.adjective()}-${fakerEN.word.noun()}-${fakerEN.number.int({max: 9999})}`
        },
        handleGenerate() {
            this.username = this.generateRandomUserName()
        },
        handleCopy() {
            navigator.clipboard.writeText(this.username)
        },
    },
})
</script>

<template>
    <div class="center-page">
        <div class="username-row" v-if="username">
            <h3 class="username">{{ username }}</h3>
            <button @click="handleCopy">Copy</button>
        </div>
        <button @click="handleGenerate">Generate Username</button>
    </div>
</template>

<style>
.center-page {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}

.username-row {
    display: flex;
    align-items: center;
    gap: 8px;
    margin-bottom: 16px;
}

.username {
    margin: 0;
    min-width: 200px;
}
</style>
