<template>
  <div id="app">
    <div v-if="userData">

      <h2><span>SIGAN A </span>{{ userData.nickname }}</h2>
      <img :src="userData.avatarLarger" alt="Foto de perfil del usuario" />
      <p>Seguidores: {{ followers }}</p>
    </div>
    <div v-else>
      <p>Cargando datos del usuario...</p>
    </div>
    <input type="text" v-model="entrada" placeholder="Nombre de usuario" />
    <button @click="consultarCuenta">Aceptar</button>
  </div>
  <br>
  <p class="texto_bottomG">Envía cualquier regalo y pondré tu cuenta para que todos vayan a seguirte</p>
  <p class="texto_bottomM">Estoy probando una API de rapidapi con Vue.JS, apoyen para hacer contenido de buena calidad sobre programación</p>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      username: 'franpaldev',
      entrada: '',
      userData: null,
      followers: null
    };
  },
  mounted() {
    this.cargarDatos(this.username);
  },
  methods: {
    consultarCuenta() {
      if (this.entrada.trim()) {
        this.username = this.entrada.trim();
        this.userData = null; // Limpia antes de nueva carga
        this.followers = null;
        this.cargarDatos(this.username);
      }
    },
    cargarDatos(usuario) {
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

      xhr.open('GET', `https://tiktok-api23.p.rapidapi.com/api/user/info?uniqueId=${usuario}`);
      xhr.setRequestHeader('x-rapidapi-key', 'f776ec5999msh94eaaca6881117dp198d62jsn24dd1768227c');
      xhr.setRequestHeader('x-rapidapi-host', 'tiktok-api23.p.rapidapi.com');
      xhr.send(data);
    }
  }
};
</script>

<style scoped>

@import url('https://fonts.googleapis.com/css2?family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&display=swap');


#app {
  max-width: 320px;
  margin: 2rem auto;
  margin-bottom: 5px;
  padding: 1.5rem;
  border-radius: 16px;
  background: linear-gradient(145deg, #ffffff, #f2f2f2);
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.08);
  text-align: center;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  transition: transform 0.3s ease;
}

#app:hover {
  transform: scale(1.1);
}

img {
  width: 170px;
  height: 170px;
  object-fit: cover;
  border-radius: 50%;
  border: 3px solid #ff0050;
  margin-bottom: 1rem;
}

h2 {
  font-size: 2.5em;
  margin: 10px;
  font-size: 1.5rem;
  color: #333;
}

p {
  margin: 0.5rem 0;
  color: #666;
  font-size: 2rem;
  font-weight: bold;
}

input {
  width: 90%;
  margin-top: 1rem;
  padding: 0.5rem;
  border-radius: 8px;
  border: 1px solid #ccc;
  outline: none;
}

button {
  margin-top: 0.8rem;
  padding: 0.5rem 1rem;
  background-color: #ff0050;
  color: #fff;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-weight: bold;
}

button:hover {
  background-color: #e10046;
}

.texto_bottomG {
  font-family: 'Inter', 'Helvetica Neue', sans-serif;
  font-size: 1.4rem;
  color: #0a0a0a;
  background: linear-gradient(135deg, #a7e4d5, #d9f5ec);
  padding: 20px 24px;
  margin-top: 1rem;
  border-radius: 12px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.08);
  line-height: 1.6;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.texto_bottomG:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
}

.texto_bottomM {
  font-family: 'Segoe UI', sans-serif;
  font-size: 1rem;
  color: #222;
  background: linear-gradient(135deg, #e0e0e0, #f5f5f5);
  padding: 22px 26px;
  margin-top: 1.5rem;
  border-radius: 12px;
  box-shadow: 0 6px 18px rgba(0, 0, 0, 0.06);
  line-height: 1.6;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.texto_bottomM:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 22px rgba(0, 0, 0, 0.08);
}

span{
  border-radius: 10px;
  background-color: #a11944;
  color: white;
  padding: 5px;
  margin-right: 5px;
}

@media (max-width: 400px) {
  #app {
    padding: 1rem;
  }

  img {
    width: 100px;
    height: 100px;
  }
}
</style>