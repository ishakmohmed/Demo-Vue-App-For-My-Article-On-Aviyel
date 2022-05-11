<template>
  <form @submit.prevent="sendFile" enctype="multipart/form-data">
    <div class="field">
      <label for="file" class="label">Upload File</label>
      <input type="file" ref="file" @change="selectFile" />
    </div>
    <div class="field">
      <button class="button-is-info">Send</button>
    </div>
  </form>
</template>

<script>
import axios from "axios";
export default {
  name: "SimpleUpload",
  data() {
    return {
      file: "",
    };
  },
  methods: {
    selectFile() {
      this.file = this.$refs.file.files[0];
    },
    async sendFile() {
      const formData = new FormData();
      const headers = {
        Authorization:
          "f25403a7784b2eb56f5759ddfe0fb3f5663db4a3de9f404919158efdf3073446",
      };
      formData.append("file", this.file);

      try {
        await axios.post("http://localhost:8000/api/v1/upload", formData, {
          headers,
        });
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>
