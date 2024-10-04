<template>
  <div class="photo-grid">
    <LoadingPlaceholder v-if="!photos.length" />
    <div
      v-for="photo in photos"
      :key="photo.id"
      class="photo-item"
      @click="openPhoto(photo)"
    >
      <div class="overlay">
        <p>{{ photo.user.name }}</p>
        <p>{{ photo.user.location || 'Location not available'}}</p>
      </div>
      <img :src="photo.urls.full" :alt="photo.alt_description" />
    </div>
  </div>
</template>

<script>
import LoadingPlaceholder from './LoadingPlaceholder.vue';

export default {
  components: { LoadingPlaceholder },
  props: {
    photos: Array,
  },
  methods: {
    openPhoto(photo) {
      this.$emit('open-modal', photo);
    },
  },
};
</script>

<style scoped>
.photo-grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 3rem; 
  justify-content: space-between; 
  position: absolute;
  top: 180px;
  width: 100%;
  margin: 0 auto;
  padding: 0 9.5rem;
}

.photo-item {
  flex: 1 1 calc(33.33% - 10px); 
  position: relative;
  margin-bottom: 10px; 
  overflow: hidden; 
  border-radius: 10px;
  width: 100%
}

.photo-item:nth-child(1) {
  flex: 1 1 calc(33.33% - 10px); 
  height: 350px; 
}
.photo-item:nth-child(2) {
  flex: 1 1 calc(33.33% - 10px); 
  height: 450px; 
}
.photo-item:nth-child(3){
      flex: 1 1 calc(33.33% - 10px); 
  height: 400px; 
}


.photo-item:nth-child(4){
  flex: 1 1 calc(33.33% - 10px);
  height: 400px; 
  top: -100px;
}
.photo-item:nth-child(5) {
  flex: 1 1 calc(33.33% - 10px);
  height: 350px; 
}
.photo-item:nth-child(6) {
  flex: 1 1 calc(33.33% - 10px); 
  height: 400px; 
    top: -50px;
}

.photo-item:nth-child(7){
  flex: 1 1 calc(33.33% - 10px); 
  height: 400px; 
    top: -100px;
}
.photo-item:nth-child(8){
  flex: 1 1 calc(33.33% - 10px); 
  height: 450px; 
    top: -50px;
}


.photo-item img {
  width: 100%;
  height: 100%; 
  object-fit: cover; 
  display: block; 
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0; 
  background: rgba(0, 0, 0, 0.5);
  color: white;
  display: flex;
  flex-direction: column; 
  justify-content: flex-end; 
  padding: 2rem; 
  width: 100%; 
}

@media (max-width: 768px) {
    .photo-grid{
        padding: 0 1.5rem;
        gap: 2.5rem;
    }
  .photo-item {
    flex: 1 1 calc(50% - 10px);
  }
  .photo-item img{
    width:100%
  }
}

@media (max-width: 480px) {
    .photo-grid{
        padding: 0 1.5rem;
        grid-template-columns: 1fr;

        width: 100%;
        margin: 0 auto;
    }
    .photo-item img{
        width: 100%;
        height: 350px;
    }
  .photo-item {
    flex: 1 1 100%; 
    width: 100%;
    height: 300px;
    top:0
   
  }
  .photo-item:nth-child(2),.photo-item:nth-child(3),.photo-item:nth-child(4),.photo-item:nth-child(5),.photo-item:nth-child(6),.photo-item:nth-child(7),.photo-item:nth-child(8){
    height: 350px;
    top:0
  }

  .overlay{
    width: 100%;
    height: 350px;
  }
 
}




</style>
