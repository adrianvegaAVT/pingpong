<template>
    <div>
        <h1>{{equipo1}} vs {{equipo2}}</h1>
        <h2>{{puntosEquipo1}} - {{puntosEquipo2}}</h2>
        <button @click="puntoEquipo1">Punto {{equipo1}}</button>
        <button @click="puntoEquipo2">Punto {{equipo2}}</button>
    </div>
</template>

<script>
export default {
  data() {
    return {
      puntosEquipo1: localStorage.getItem('puntosEquipo1') || 0,
      puntosEquipo2: localStorage.getItem('puntosEquipo2') || 0,
      equipo1: this.$route.query.equipo1,
      equipo2: this.$route.query.equipo2
    }
  },
  methods: {
    puntoEquipo1() {
      this.puntosEquipo1++
      localStorage.setItem('puntosEquipo1', this.puntosEquipo1)
    },
    puntoEquipo2() {
      this.puntosEquipo2++
      localStorage.setItem('puntosEquipo2', this.puntosEquipo2)
    }
  }
}
</script>