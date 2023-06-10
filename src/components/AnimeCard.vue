<template>
  <b-card
    :title="anime.title"
    :img-src="anime.imgUrl"
    :img-alt="`${anime.title}-Image`"
    img-top
    style="max-width: 20rem"
    class="mb-2"
  >
    <b-card-text> Number of episodes: {{ anime.episodes }} </b-card-text>
    <b-card-text> Status: {{ anime.status }} </b-card-text>

    <b-button @click="editAnime" variant="outline-primary">Edit</b-button>

    <!-- Edit Modal -->
    <b-modal v-model="showEditModal" title="Edit Anime">
      <b-form-input v-model="editedAnime.title" type="text" placeholder="Enter the title"></b-form-input>
      <b-form-input v-model="editedAnime.episodes" type="number" placeholder="Enter number of episodes"></b-form-input>
      <b-form-select v-model="editedAnime.status" :options="statusOptions" placeholder="Select status"></b-form-select>
      <b-form-input v-model="editedAnime.imgUrl" type="url" placeholder="Enter the image URL"></b-form-input>

      <template #modal-footer>
        <b-button @click="saveChanges" variant="primary">Save Changes</b-button>
        <b-button @click="closeEditModal" variant="secondary">Close</b-button>
      </template>
    </b-modal>
  </b-card>
</template>

<script>
export default {
  props: {
    anime: {
      type: Object,
      default: function () {
        return {
          title: "",
          episodes: 0,
          status: null,
          imgUrl: "",
        };
      },
    },
  },
  data() {
    return {
      showEditModal: false,
      editedAnime: {},
      statusOptions: ["OnGoing", "Finished"],
    };
  },
  methods: {
    editAnime() {
      // Set the editedAnime data to the current anime object
      this.editedAnime = { ...this.anime };
      this.showEditModal = true;
    },
    saveChanges() {
      // Save the changes made to the editedAnime data
      // You can dispatch an action or perform any necessary operations here
      // For simplicity, we'll just emit an event with the edited anime data
      this.$emit("edit-anime", this.editedAnime);
      this.showEditModal = false;
    },
    closeEditModal() {
      this.showEditModal = false;
    },
  },
};
</script>


