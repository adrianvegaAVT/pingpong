<template>
	<div class="col-sm-12 col-xl-3 col-lg-3 col-md-6 p-4 mx-auto my-auto">
		<div class="d-flex justify-content-end">
			<img class="img-log" src="img/local/uped-logo.png" alt="" />
		</div>
		<div class="mt-4">
			<label for="" class="fs-2 fw-bold">Equipo / Jugador 1</label>
			<input
				type="text"
				id="equipo1"
				v-model="equipo1"
				class="form-control mt-3"
			/>
		</div>
		<div class="mt-4 mb-4">
			<label for="" class="fs-2 fw-bold">Equipo / Jugador 2</label>
			<input
				type="text"
				id="equipo2"
				v-model="equipo2"
				class="form-control mt-3"
			/>
		</div>
		<div class="mt-4 d-flex justify-content-center">
			<button
				type="button"
				@click="iniciarJuego"
				class="btn btn-primary mt-4 btn-iniciar-juego"
			>
				Iniciar Juego
			</button>
		</div>
		<p>{{ error }}</p>
	</div>
</template>

<script>
export default {
	data() {
		return {
			equipo1: "",
			equipo2: "",
			error: "",
		};
	},
	methods: {
		iniciarJuego() {
			if (!this.equipo1 || !this.equipo2) {
				this.error = "Por favor, introduce los nombres de ambos equipos";
				return;
			}

			localStorage.setItem("puntosEquipo1", 0);
			localStorage.setItem("puntosEquipo2", 0);
			localStorage.setItem("equipo1Sets", 0);
			localStorage.setItem("equipo2Sets", 0);
			this.$router.push({
				name: "game",
				query: {
					equipo1: this.equipo1,
					equipo2: this.equipo2,
				},
			});
		},
	},
};
//modificacion de prueba
</script>
