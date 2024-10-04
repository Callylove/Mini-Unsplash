<template>
  <div id="app">
    <header>
      <div class="search-container">
        <input
          v-if="!isLoading && !hasResults"
          type="text"
          v-model="searchQuery"
          placeholder="Search for photo"
          @input="fetchPhotos"
        />  
        <span class="search-icon" v-if="!isLoading && !hasResults">
          <i class="fa fa-search" aria-hidden="true"></i>
        </span>
        <p v-if="isLoading" class="search-results">{{ loadingMessage }}</p>
        <p v-if="!isLoading && hasResults" class="search-results">Search Results for <span class="result">"{{ searchQuery }}"</span></p>
      
      </div>
    </header>
    <div>
      <LoadingPlaceholder v-if="isLoading" />
      <PhotoGrid v-if="photos.length && !isLoading" :photos="photos" @open-modal="openModal" />
      <PhotoModal v-if="selectedPhoto" :photo="selectedPhoto" @close="selectedPhoto = null" />
    </div>
  </div>
</template>

<script>
import PhotoGrid from './components/PhotoGrid.vue';
import PhotoModal from './components/PhotoModal.vue';
import LoadingPlaceholder from './components/LoadingPlaceholder.vue';
import axios from 'axios';

export default {
  components: { PhotoGrid, PhotoModal, LoadingPlaceholder },
  data() {
    return {
      photos: [],
      searchQuery: '',
      hasResults: false,
      selectedPhoto: null,
      isLoading: false,
      loadingMessage: ''
    };
  },
  mounted() {
    this.fetchAfricanPhotos();
  },
  methods: {
    async fetchAfricanPhotos() {
      this.isLoading = true;
      this.loadingMessage = 'Loading African photos...';
      try {
        const response = await axios.get(`https://api.unsplash.com/search/photos`, {
          params: {
            query: 'African',
            client_id: 'sH9vfJQXKaBuY-Z9EH32B8XXOb9nnT3lGhjn9VIEpjc', 
            per_page: 8,
          },
        });
        this.photos = response.data.results;
      } catch (error) {
        console.error(error);
      } finally {
        this.isLoading = false;
      }
    },
    async fetchPhotos() {
      if (!this.searchQuery) {
        await this.fetchAfricanPhotos();
        this.hasResults = false; 
        return;
      }
      if (this.searchQuery.length < 3) {
      this.photos = []; 
      this.hasResults = false; 
      return; 
    }

      this.isLoading = true;
      this.loadingMessage = `Searching for "${this.searchQuery}"...`;

      try {
        const response = await axios.get(`https://api.unsplash.com/search/photos`, {
          params: {
            query: this.searchQuery,
            client_id: 'sH9vfJQXKaBuY-Z9EH32B8XXOb9nnT3lGhjn9VIEpjc', 
          },
        });
        this.photos = response.data.results;
        this.hasResults = this.photos.length > 0; 
      } catch (error) {
        console.error(error);
      } finally {
        this.isLoading = false;
      }
    },
    openModal(photo) {
      this.selectedPhoto = photo;
    },
  },
};
</script>

<style>
.search-container {
  background: rgba(255, 255, 255, 0.8);
  position: relative;
  /* margin: 0 auto; */
  width: 100%;
  background-color: rgb(203, 213, 225);
  height: 220px;
  display: flex;
  justify-content: flex-start;
  align-items: flex-start;
}

.search-container input {
  width: 90%;
  height: 50px;
  border: 1px solid #fff;
  border-radius: 5px;
  margin-bottom: 20px;
  background: #fff;
  padding: 12px 64px;
  position: relative;
  align-self: center;
  justify-self: center;
 margin: 2rem auto;

  
}

.search-container input:focus {
  border-color: rgb(203, 213, 225);
  outline: none;
}

.search-icon .fa {
  position: absolute;
  left: 85px;
  top: 50%;
  transform: translateY(-50%);
  font-size: 16px;
  pointer-events: none;
}

.loading {
  text-align: center;
  font-size: 18px;
  margin: 20px 0;
}
.search-results{
  align-self: flex-start;
  justify-self: flex-start;
  padding-left: 5rem;
  margin-top: 3rem;
  font-size: 2rem;
  font-weight: 500;
  color: rgb(51 65 85);

}
.result{
  color: rgb(100 116 139);
  text-transform: capitalize;
}
@media (max-width: 768px) {
  .search-icon .fa {
    left: 60px;
  }
}

@media (max-width: 480px) {
  .search-icon .fa {
    left: 50px;
  }
}
</style>
