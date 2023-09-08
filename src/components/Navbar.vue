<template>
    <header class="header">
        <nav class="header__nav" v-if="nav">
            <button class="header__nav-lang">Ru</button>
            <h1 class="header__nav-title">Заметки</h1>
            <button class="header__nav-search" @click="nav = false">
                <img src="@/assets/images/search.svg" alt="">
            </button>
        </nav>
        <nav class="header__search" v-else>
            <button class="header__search-back" @click="text = '', nav = true">
                <img src="@/assets/images/back.svg" alt="">
            </button>
            <input v-model="text" type="text" class="header__search-input" placeholder="Поиск...">
            <button class="header__search-clear" @click="text = ''">
                <img src="@/assets/images/close.svg" alt="">
            </button>
        </nav>
    </header>
</template>

<script>
    export default {
        data() {
            return {
                text: '',
                nav: true
            }
        },
        watch: {
            text(newVal) {
                this.$emit('setSearch', newVal)
            }
        }
    }
</script>

