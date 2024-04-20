<template>
  <div>
    <h1 class="container">Image Upload Vue.js</h1>
    <div>
      <div class="file-container">
        <div>
          <form>
            <input
              type="file"
              id="media"
              accept="image/*"
              multiple
              @change="(event) => handelFileUpload(event)"
            />
            <div>
              <section>
                <img src="./assets/upload.svg" />
                <p>Upload Your answer here.</p>
              </section>
            </div>
          </form>
        </div>
      </div>
      <div>
        <div class="imgages">
          <div
            v-for="(src, index) in imageSrc"
            :key="index"
            class="images-lists"
          >
            <div class="image-container">
              <img :src="src" id="output" class="image-style" />
            </div>
            <div class="cross-icon" v-if="imageSrc">
              <img src="./assets/cancel.svg" @click="removeItem(index)" />
            </div>

            <p style="width: 150px" class="line-clamp-1 text-center">
              {{ selectedFiles[index].name }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";

const form = ref({
  media: {},
});

const imageSrc = ref([]);

const selectedFiles = ref([]);
const handelFileUpload = (e) => {
  var files = e.target.files || e.dataTransfer.files;
  if (!files.length) return;

  for (let i = 0; i < files.length; i++) {
    selectedFiles.value.push(files[i]);
    const src = URL.createObjectURL(files[i]);
    imageSrc.value.push(src);
  }
  console.log(selectedFiles.value, "seldjhfdh fikes");

  form.value.media = e.target.files[0];
  console.log(form.value.media, "file upload");

  console.log("files already uploaded", imageSrc.value);
};

const removeItem = (index) => {
  imageSrc.value.splice(index, 1);
};
</script>
<style>
.container {
  margin-bottom: 40px;
  display: flex;
  flex-direction: column;
}
.file-container {
  position: relative;
  cursor: pointer;
}
form {
  width: 500px !important;
  position: absolute;
  top: 55%;
  left: 0;
  margin-top: -100px;
  width: 100%;
  height: 90px;
  border-radius: 5px;
  border: 1.5px dashed #a0a0a0;
  cursor: pointer;
}
form div {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
form input {
  position: absolute;
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  outline: none;
  opacity: 0;
}
form button {
  margin: 0;
  color: #fff;
  background: #16a085;
  border: none;
  width: 508px;
  height: 35px;
  margin-top: -20px;
  margin-left: -4px;
  border-radius: 4px;
  border-bottom: 4px solid #117a60;
  transition: all 0.2s ease;
  outline: none;
}
form button:hover {
  background: #149174;
  color: #0c5645;
}
form button:active {
  border: 0;
}

.imgages {
  position: relative;
  margin-top: 100px;
  display: flex;
  flex-direction: row;
  justify-content: center;
}

.images-lists {
  position: relative;
  margin-left: 10px;
  margin-right: 10px;
}

.image-container {
  padding: 4px;
  border: 0.5px solid #a0a0a0;
  border-radius: 10px;
}

.image-style {
  height: 150px;
  width: 150px;
  object-fit: cover;
}

.cross-icon {
  position: absolute;
  top: 0%;
  right: 0;
  cursor: pointer;
}
</style>
