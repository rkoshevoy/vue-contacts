<template>
  <div id="app">
      <div class="contacts-wrapper" >
        <contacts
          ref="contacts"
          @addContactShow="showAddModal"
          @editContactShow="showEditModal" />

        <add-edit-modal
          ref="modal"
          v-show="showModal"
          @modalHide="modalHide"
          @addContact="addContact"
          @editContact="editContact" />
      </div>
  </div>
</template>

<script>
import Contacts from './components/Contacts'
import AddEditModal from './components/AddEditModal'

export default {
  name: 'App',
  components: {
    Contacts,
    AddEditModal
  },
  data() {
    return {
      showModal: false
    }
  },
   methods: {
     showAddModal() {
        this.$refs.modal.addContactShow();
        this.showModal = true;
     },

     showEditModal(contactInfo) {
        this.$refs.modal.editContactShow(contactInfo, this.$refs.contacts.contactsList.indexOf(contactInfo));
        this.showModal = true;
     },

     addContact(newContactInfo) {
       this.$refs.contacts.addContact(newContactInfo);
       this.$refs.modal.clearInputs();
       this.modalHide();
     },

     editContact(editableContactInfo) {
       this.$refs.contacts.editContact(editableContactInfo[0], editableContactInfo[1]);
       this.modalHide();
     },

      modalHide() {
        this.showModal = false;
      },

      scrollHanle(evt) {
        console.log(evt)
      }
   }
}
</script>

<style lang="scss">

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    outline: none;
  }

  body {
    min-width: 320px;
    font-family: 'Open Sans', sans-serif;
    font-size: 14px;
  }

  ul {
    list-style: none;
  }

  .contacts-wrapper {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    width: 100vw;
    height: 100vh;
    margin: 0 auto;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .3s;
  }
  .fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
    opacity: 0;
  }
</style>
