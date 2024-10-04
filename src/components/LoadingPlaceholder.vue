<template>
 <div class="loading-placeholder">
    <div class="placeholder" v-for="n in 8" :key="n">
      <div class="placeholder-image"></div>
      <div class="placeholder-text-longer"></div>
      <div class="placeholder-text-shorter"></div>
    </div>
  </div>
</template>

<style scoped>
.loading-placeholder {
display: grid;
  grid-template-columns: 1fr 1fr 1fr;

  gap: 3rem; 
  justify-content: space-between; 
  position: absolute;
  top: 150px;
  width: 100%;
  margin: 0 auto;
  padding: 0 9.5rem;
}

.placeholder {
flex: 1 1 calc(33.33% - 10px); 
  position: relative;
  margin-bottom: 10px;
  overflow: hidden; 
  border-radius: 10px;
  width: 100%
}
.placeholder:nth-child(1){
    flex: 1 1 calc(33.33% - 10px); 
  height: 350px; 
}
.placeholder:nth-child(2){
    flex: 1 1 calc(33.33% - 10px); 
  height: 450px; 
}
.placeholder:nth-child(3){
    flex: 1 1 calc(33.33% - 10px); 
  height: 400px; 
}
.placeholder:nth-child(4){
   flex: 1 1 calc(33.33% - 10px);
  height: 400px; 
  top: -100px;
}
.placeholder:nth-child(5){
    flex: 1 1 calc(33.33% - 10px);
  height: 350px; 
}
.placeholder:nth-child(6){
     flex: 1 1 calc(33.33% - 10px); 
  height: 400px; 
    top: -50px;
}
.placeholder:nth-child(7){
  flex: 1 1 calc(33.33% - 10px); 
  height: 400px; 
    top: -100px;
}
.placeholder:nth-child(8){
      flex: 1 1 calc(33.33% - 10px); 
  height: 450px; 
    top: -50px;
}
.placeholder-image {
  width: 100%;
  height: 100%; 
  object-fit: cover; 
  display: block; 
  background-color: rgb(241 245 249); 
}

.placeholder-text-longer {
  position: absolute;
  bottom: 10px; 
  left: 10px; 
  right: 10px; 
  width: calc(40% - 20px); 
  background-color: rgb(226, 232, 240); 
  color: rgb(100, 100, 100); 
  padding: 5px; 
  border-radius: 4px; 
  margin-bottom: 25px; 
}

.placeholder-text-shorter {
  position: absolute;
  bottom: 20px; 
  left: 10px; 
  right: 10px; 
  width: calc(20% - 20px); 
  background-color: rgb(226, 232, 240); 
  color: rgb(100, 100, 100);
  padding: 5px; 
  border-radius: 4px; 
}

@keyframes pulse {
  0% {
    background: #eee;
  }
  50% {
    background: #ddd;
  }
  100% {
    background: #eee;
  }
}
</style>
