<template>
  <div v-if="userData">
    <h2>{{ userData.nickname }}</h2>
    <img :src="userData.avatarLarger" alt="Foto de perfil del usuario" width="150" />
    <p>Seguidores: {{ followers }}</p>
  </div>
  <div v-else>
    <p>Cargando datos del usuario...</p>
  </div>
</template>

<script>
export default {
  name: 'UsuarioTikTok',
  props: {
    username: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      userData: null,
      followers: null
    };
  },
  mounted() {
    const data = null;
    const xhr = new XMLHttpRequest();
    xhr.withCredentials = true;

    xhr.addEventListener('readystatechange', () => {
      if (xhr.readyState === XMLHttpRequest.DONE) {
        try {
          const response = JSON.parse(xhr.responseText);
          this.userData = response.userInfo.user;
          this.followers = response.userInfo.stats.followerCount;
        } catch (e) {
          console.error('Error al parsear datos:', e);
        }
      }
    });

    xhr.open('GET', `https://tiktok-api23.p.rapidapi.com/api/user/info?uniqueId=${this.username}`);
    xhr.setRequestHeader('x-rapidapi-key', 'f776ec5999msh94eaaca6881117dp198d62jsn24dd1768227c');
    xhr.setRequestHeader('x-rapidapi-host', 'tiktok-api23.p.rapidapi.com');
    xhr.send(data);
  }
};
</script>

<style scoped>
div {
  max-width: 320px;
  margin: 2rem auto;
  padding: 1.5rem;
  border-radius: 16px;
  background: linear-gradient(145deg, #ffffff, #f2f2f2);
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.08);
  text-align: center;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  transition: transform 0.3s ease;
}
div:hover {
  transform: scale(1.02);
}
img {
  width: 120px;
  height: 120px;
  object-fit: cover;
  border-radius: 50%;
  border: 3px solid #ff0050;
  margin-bottom: 1rem;
}
h2 {
  margin: 10px;
  font-size: 1.5rem;
  color: #333;
}
p {
  margin: 0.5rem 0;
  color: #666;
  font-size: 1rem;
  font-weight: bold;
}
@media (max-width: 400px) {
  div {
    padding: 1rem;
  }
  img {
    width: 100px;
    height: 100px;
  }
}
</style>
