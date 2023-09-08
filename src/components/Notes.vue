<template>
    <div class="notes">
        <div class="container">
            <div class="notes__head">
                <h2 class="notes__head-title">
                    {{ notes.length > 0 ? 'Все заметки' : 'Нет заметок' }}
                </h2>
                <button class="notes__head-btn" @click="view = !view">
                    <img v-show="view" src="@/assets/images/list.svg" alt="">
                    <img v-show="!view" src="@/assets/images/grid.svg" alt="">
                    <span>{{ view ? 'Список' : 'Сетка' }}</span>
                </button>
            </div>
            <div class="notes__list" :class="{active: !view}">
                <NotesItem
                    v-for="note in notes"
                    :key="note.id"
                    :note="note"
                    :view="view"
                    @delNote="$emit('delNote', note)"
                    @change="$emit('change', note)"
                />
            </div>
        </div>
    </div>
</template>

<script>
import NotesItem from './NotesItem.vue';

    export default {
    props: {
      notes: {
        type: Array
      }  
    },
    data() {
        return {
            view: true
        };
    },
    components: { NotesItem }
}
</script>

