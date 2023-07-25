
<template>
  <div class="text-white wrapper d-flex justify-content-center align-items-center width bg-dark">
    <div class="row">
      <div class="col">
        <div class="row">
          <div class="col">
            <div class="mb-3">
              <label class="form-label"> Type </label>
              <select v-model="selectedTypes" class="form-select form-select-lg">
                <option disabled value="">Type</option>
                <option value="sfw/">SFW (Safe For Work)</option>
                <option value="nsfw/">NSFW (Not Safe Forasdasd Work)</option>

              </select>
            </div>
          </div>
          <div class="col">
            <div v-if="selectedTypes == ''" class="mb-3">
              <label class="form-label">Category</label>
              <select class="form-select form-select-lg">
                <option disabled value="Silahkan pilih type">Silahkan Pilih Type</option>
              </select>
            </div>
            <div v-else-if="selectedTypes == 'sfw/'" class=" mb-3">
              <label class="form-label">Category</label>
              <select v-model="category" class="form-select form-select-lg">
                <option disabled value="">Pilih Category</option>
                <option value="waifu">Waifu</option>
                <option value="blush">Blush</option>
                <option value="nom">Nom</option>
              </select>
            </div>
            <div v-else-if="selectedTypes == 'nsfw/'" class=" mb-3">
              <label class="form-label">Mesum Kali Otak Kau</label>
              <select class="form-select form-select-lg">
                <option>Dasar Mesum!</option>
              </select>
            </div>
          </div>
        </div>
        <div class="row">
          <div class="col d-flex flex-column">
            <img :src="imageUrl" alt=""><br>
            <button v-if="isLoading" class="btn btn-primary" type="button" disabled>
              <span class="spinner-border spinner-border-sm" role="status" aria-hidden="true"></span>
              Loading...
            </button>
            <button v-else-if="selectedTypes == '' || selectedTypes == 'nsfw/' || category == ''" @click="getImage()"
              type="button" class="btn disabled btn-primary">Pilih Type Terlebih Dahulu</button>
            <button v-else @click="getImage()" type="button" class="btn btn-primary">GetImage!</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios"
export default {
  data() {
    return {
      imageUrl: null,
      isLoading: false,
      selectedTypes: "",
      category: ""
    }
  },
  methods: {

    async getImage() {
      const url = "https://api.waifu.pics/"
      this.isLoading = true
      await axios.get(url + this.selectedTypes + this.category).then((response) => {
        console.log(response.data.url)
        this.imageUrl = response.data.url

      })
        .catch((err) => {
          alert(err)
        })
      this.isLoading = false
    }
  }
}
</script>

<style scoped>
.wrapper {
  height: 100vh;

}

img {
  width: 50rem;
  height: 25rem;
}
</style>
