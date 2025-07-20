<script lang="ts">
import { fakerEN } from "@faker-js/faker"
import { defineComponent } from "vue"

export enum CaseType {
    Lower = "lower",
    Upper = "upper",
    Title = "title",
}

export default defineComponent({
    data() {
        return {
            username: "",
            caseType: CaseType.Lower,
            separator: "-",
        }
    },
    methods: {
        generateRandomUserName() {
            const adj = fakerEN.word.adjective()
            const noun = fakerEN.word.noun()
            const num = fakerEN.number.int({ max: 9999 })
            let sep = this.separator
            let adjPart = adj
            let nounPart = noun
            if (this.caseType === CaseType.Upper) {
                adjPart = adj.toUpperCase()
                nounPart = noun.toUpperCase()
            } else if (this.caseType === CaseType.Title) {
                adjPart = adj.charAt(0).toUpperCase() + adj.slice(1)
                nounPart = noun.charAt(0).toUpperCase() + noun.slice(1)
            } else {
                adjPart = adj.toLowerCase()
                nounPart = noun.toLowerCase()
            }
            return `${adjPart}${sep}${nounPart}${sep}${num}`
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
        <div class="config-row">
            Case Type:
            <div class="case-radio-group">
                <label>
                    <input type="radio" value="lower" v-model="caseType" />
                    Lower
                </label>
                <label>
                    <input type="radio" value="upper" v-model="caseType" />
                    Upper
                </label>
                <label>
                    <input type="radio" value="title" v-model="caseType" />
                    Title
                </label>
            </div>
        </div>
        <label class="config-row">
            Separator:
            <input
                type="text"
                v-model="separator"
                class="separator-input"
                maxlength="2"
            />
        </label>
    </div>
</template>

<style>
.center-page {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    min-height: 100svh;
    gap: 8px;
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

.separator-input {
    width: 40px;
}

.case-radio-group {
    display: flex;
    gap: 8px;
}

.config-row {
    gap: 16px;
    display: flex;
    align-items: center;
}
</style>
