<template>
    <div class="modal" @click="closeModal">
        <div class="modal__block" @click.stop>
            <h2 class="modal__block-title">
                {{  isEdit ? 'Изменить заметку' : 'Добавить заметку' }}
            </h2>
            <div class="modal__block-inputs">
                <label>
                    <span>Title</span>
                    <input v-model="title" type="text" placeholder="Title">
                </label>
                <label>
                    <span>Content</span>
                    <textarea v-model="text" placeholder="Content"></textarea>
                </label>
            </div>
            <div class="modal__block-btns">
                <button class="modal__block-btns-btn red" @click="closeModal">Отмена</button>
                <button v-if="!isEdit" class="modal__block-btns-btn purple" @click="addNote">Добавить</button>
                <button @click="changeNote" v-if="isEdit" class="modal__block-btns-btn purple">Изменить</button>
            </div>
        </div>
    </div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid';
    export default {
        props: {
            isEdit: {
                type: Boolean
            },
            editNote: {
                type: Object
            }
        },
        data() {
            return {
                title: '',
                text: ''
            }
        },
        created() {
            this.title = this.editNote?.title
            this.text = this.editNote?.text
        },
        methods: {
            closeModal() {
                this.$emit('close')
            },
            changeNote() {
                if(this.text.length > 2 && this.title.length > 2) {
                    const newNote = {
                        id: this.editNote.id,
                        title: this.title,
                        text: this.text,
                        date: new Date().toLocaleDateString()
                    }
                    this.$emit('changeNote', newNote)
                    this.closeModal()
                }
            },
            addNote() {
                if(this.text.length > 2 && this.title.length > 2) {
                    const note = {
                    id: uuidv4(),
                    title: this.title,
                    text: this.text,
                    date: new Date().toLocaleDateString()
                    }
                    this.$emit('addNote', note)
                    this.closeModal()
                }
               
            }
        },
    }
</script>

