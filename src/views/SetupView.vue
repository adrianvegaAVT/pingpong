<template>
    <div>
        <label for="">Equipo / Jugador 1</label>
        <input type="text" id="equipo1" v-model="equipo1" />
    </div>
    <div>
        <label for="">Equipo / Jugador 2</label>
        <input type="text" id="equipo2" v-model="equipo2"/>
    </div>
    <button type="button" @click="iniciarJuego">Iniciar Juego</button>
    <p>{{error}}</p>
</template>

<script>
export default {
  data() {
    return {
      equipo1: '',
      equipo2: '',
      error: ''
    }
  },
  methods: {
    iniciarJuego() {
      if (!this.equipo1 || !this.equipo2) {
        this.error = 'Por favor, introduce los nombres de ambos equipos';
        return;
      }

      localStorage.setItem('puntosEquipo1', 0);
      localStorage.setItem('puntosEquipo2', 0);
      this.$router.push({
        name: 'game',
        query: {
          equipo1: this.equipo1,
          equipo2: this.equipo2
        }
      })
    }
  }
}
</script>
