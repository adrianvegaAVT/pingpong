<template>
	<div class="col-sm-12 col-xl-3 col-lg-3 col-md-6 m-4">
		<div class="d-flex justify-content-between align-items-center">
			<div>
				<a class="btn btn-secondary" href="/">Regresar</a>
			</div>
			<img class="img-log" src="img/local/uped-logo.png" alt="" />
		</div>

        <div class="div-set-num">
            <p class="h1 p-4 text-center">Set #</p>
        </div>

        <div class="div-puntaje rounded p-3" >
            <p class="h4 text-center bold">Puntos</p>
            <div class="d-flex justify-content-around">
                <div>
                    <p class="points text-center">{{ puntosEquipo1 }}</p>
                    <button class="mx-auto">+</button>
                </div>
                <div>
                    <p class="points text-center">{{ puntosEquipo2 }}</p>
                    <button>+</button>
                </div>
            </div>
        </div>

		<h1>{{ equipo1 }} vs {{ equipo2 }}</h1>
		<h2>{{ puntosEquipo1 }} - {{ puntosEquipo2 }}</h2>
		<button @click="puntoEquipo1">Punto {{ equipo1 }}</button>
		<button @click="puntoEquipo2">Punto {{ equipo2 }}</button>
	</div>
</template>

<script>
export default {
	data() {
		return {
			puntosEquipo1: localStorage.getItem("puntosEquipo1") || 0,
			puntosEquipo2: localStorage.getItem("puntosEquipo2") || 0,
			equipo1: this.$route.query.equipo1,
			equipo2: this.$route.query.equipo2,
		};
	},
	methods: {
		puntoEquipo1() {
			this.puntosEquipo1++;
			localStorage.setItem("puntosEquipo1", this.puntosEquipo1);
		},
		puntoEquipo2() {
			this.puntosEquipo2++;
			localStorage.setItem("puntosEquipo2", this.puntosEquipo2);
		},
	},
};
</script>
