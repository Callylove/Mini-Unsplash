<template>
  <div class="modal" @click.self="close">
    <button class="close-button" @click="close">&times;</button>
    <div class="card">
      <img :src="photo.urls.full" :alt="photo.alt_description" class="card-image" />
      <div class="modal-info">
        <h3>{{ photo.user.name }}</h3>
        <p>{{ photo.user.location || 'Location not available' }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    photo: Object,
  },
  methods: {
    close() {
      this.$emit('close');
    },
  },
};
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.close-button {
  position: absolute;
  top: 70px;
  right: 180px;
  background: transparent;
  border: none;
  color: white;
  font-size: 3rem;
  cursor: pointer;
  transition: color 0.3s;
}

.close-button:hover {
  color: #ffcc00; 
}

.card {
  position: relative;
  width: 90%;
  max-width: 900px; 
  max-height: 900px;
  border-radius: 10px;
  overflow: hidden;
  background: white; 
  margin-top: 90px;
}

.card-image {
  width: 100%;
  height: 500px;
  /* object-fit: cover;  */
}

.modal-info {

  bottom: 20px;
  left: 20px; 
  color: #333; 
  text-align: left;
  background: rgba(255, 255, 255, 0.8); 
  padding: 10px;
  border-radius: 4px;
  padding-left: 2rem;
  padding-bottom: 2rem;
}

.modal-info h3 {
  margin: 0;
  font-size: 1.5rem; 
  text-transform: capitalize;
}

.modal-info p {
  margin: 0;
  font-size: 1rem; 
}
@media (max-width:768px){
     .close-button{
        right: 30px;
        top: 150px;
        font-size: 3rem;
    }
}
@media (max-width: 480px){
    .card{
        max-width: 500px;
        max-height: 500px;
    }
    .close-button{
        right: 10px;
        top: 120px;
        font-size: 2rem;
    }
    .card-image{
        height: 300px;
    }
}
</style>
