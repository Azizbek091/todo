<template>
    <div class="notes__item">
        <div class="notes__item-top" :class="{active: !view}">
            <h2 class="notes__item-top-title">{{ note.title }}</h2>
            <span class="notes__item-top-date">{{ note.date }}</span>
        </div>
        <p class="notes__item-text">{{ note.text }}</p>
        <div class="notes__item-btns">
            <button class="notes__item-btns-btn purple" @click="$emit('change', note)">
                <img src="@/assets/images/edit.svg" alt="">
                <span>РЕДАКТИРОВАТЬ</span>
            </button>
            <button class="notes__item-btns-btn red" @click="$emit('delNote', note)">
                <img src="@/assets/images/del.svg" alt="">
                <span>Удалить</span>
            </button>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            note: {
                type: Object
            },
            view: {
                type: Boolean
            }
        }
    }
</script>

