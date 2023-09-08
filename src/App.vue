<template>
  <div class="wrapper">
    <Navbar @setSearch="search = $event"/>
    <Notes 
      :notes="filterNotes"
      @delNote="delNote"
      @change="change"
    />
    <Transition name="modal">
      <Modal
        :editNote="editNote"
        v-if="isModalOpen"
        @close="isModalOpen = false, editNote = null"
        @addNote="addNote"
        :isEdit="isEdit"
        @changeNote="changeNote"
      />
    </Transition>
    
    
    <button class="add" v-show="!isModalOpen" @click="isModalOpen = true, isEdit = false">
      <img src="@/assets/images/edit.svg" alt="">
    </button>
  </div>
</template>

<script>
import Modal from './components/Modal.vue';
import Navbar from './components/Navbar.vue';
import Notes from './components/Notes.vue';

  export default {
    components: {
    Navbar,
    Notes,
    Modal
  },
    data() {
      return {
        search: '',
        editNote: null,
        isEdit: false,
        isModalOpen: false,
        notes: [
          { id: 1, title: 'HTML', text: 'dasdasdasdasdasdsadas', date: '07.03.2022' },
          { id: 2, title: 'CSS', text: 'dasdasdasdasdasdsadas', date: '07.03.2022' },
          { id: 3, title: 'JS', text: 'dasdasdasdasdasdsadas', date: '07.03.2022' },
          { id: 4, title: 'Vue', text: 'dasdasdasdasdasdsadas', date: '07.03.2022' },
        ]
      }
    },
    watch: {
      notes: {
        handler(newVal) {
          localStorage.notes = JSON.stringify(this.notes)
        },
        deep: true
      }
    },
    mounted() {
      this.getNotes()
    },
    computed: {
      filterNotes() {
        return this.search ? this.notes.filter(note => note.title.toLowerCase().includes(this.search.toLowerCase()) ) : this.notes
      }
    },
    methods: {
      addNote(note) {
        this.notes.push(note)
      },
      delNote(note) {
        this.notes = this.notes.filter(el => el.id != note.id)
      },
      changeNote(newNote) {
        this.notes.forEach((note,i) => {
          if(note.id == newNote.id) {
            this.notes.splice(i,1, newNote)
          }
        })
      },
      change(note) {
       this.isModalOpen = this.isEdit = true
       this.editNote = note
      },
      getNotes() {
        if(localStorage.notes) {
          this.notes = JSON.parse(localStorage.notes)
        }
      }
    },
}
</script>

