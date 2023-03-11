<template>
  <!-- // FUTUR UPLOAD DE PHOTO DANS LA BDD A FAIRE // -->

  <div class="container mt-5">
    <form>
      <div class="custom-file">
        <input type="file" class="" id="button" />
        <!-- v-model="picture" -->
      </div>
      <!-- <button type="submit" name="submit" class="btn btn-primary btn-block mt-4">
                Upload Files
            </button> -->
    </form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      picture: "",
    };
  },

  methods: {
    async getPicture() {
      const body = {
        picture: this.picture,
      };

      const response = await fetch("http://127.0.0.1:8000/api/upload-picture", {
        methods: "POST",
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
        },
        body: JSON.stringify(body),
      });
      const data = await response.json();
      this.picture = data.picture;
    },
  },
};
</script>

<style scoped></style>
