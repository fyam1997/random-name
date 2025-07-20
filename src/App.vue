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
    <div style="display: flex; align-items: center; gap: 8px; margin-bottom: 16px;">
        <h3 style="margin: 0; min-width: 200px;">{{ username }}</h3>
        <button @click="handleCopy" :disabled="!username">Copy</button>
    </div>
    <button @click="handleGenerate">Generate Username</button>
</template>
