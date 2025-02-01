<template>
  <teleport to="body">
    <base-dialog
      @close-dialog="closeDialog"
      title="Invalid Input"
      v-if="inputIsInvalid"
    >
      <template #default>
        <p>Unfortunately, at least one input value is invalid.</p>
        <p>
          Check all inputs and make sure at least a few characters have been
          entered in each field.
        </p>
      </template>
      <template #actions>
        <base-button @click="closeDialog">Okay</base-button>
      </template>
    </base-dialog>
  </teleport>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" id="title" name="title" v-model="enteredTitle" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          id="description"
          name="description"
          rows="3"
          v-model="enteredDescription"
        />
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input type="url" id="link" name="link" v-model="enteredLink" />
      </div>
      <div>
        <base-button type="submit" @click="submitData"
          >Add Resources</base-button
        >
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseCard from '@/components/ui/BaseCard.vue';
import BaseButton from '@/components/ui/BaseButton.vue';
import BaseDialog from '@/components/ui/BaseDialog.vue';
export default {
  inject: {
    addNewResource: {
      type: Function,
      required: true,
    },
  },
  components: {
    BaseDialog,
    BaseCard,
    BaseButton,
  },
  data() {
    return {
      enteredTitle: '',
      enteredDescription: '',
      enteredLink: '',
      inputIsInvalid: false,
    };
  },
  methods: {
    closeDialog() {
      this.inputIsInvalid = false;
    },
    submitData() {
      const newResource = {
        id: new Date().toISOString(),
        title: this.enteredTitle,
        description: this.enteredDescription,
        link: this.enteredLink,
      };

      if (
        newResource.title.trim() === '' ||
        newResource.description.trim() === '' ||
        newResource.link.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }

      this.addNewResource(newResource);
      this.enteredTitle = '';
      this.enteredDescription = '';
      this.enteredLink = '';
    },
  },
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
