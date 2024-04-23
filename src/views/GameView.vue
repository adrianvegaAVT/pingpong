<template>
	<div class="col-sm-12 col-xl-3 col-lg-3 col-md-6 m-4">
		<div class="d-flex justify-content-between align-items-center">
			<div>
				<a class="btn btn-secondary" href="/">Finalizar</a>
			</div>
			<img class="img-log" src="img/local/uped-logo.png" alt="" />
		</div>

        <div class="div-set-num">
            <p class="h1 p-4 text-center fw-bold">Set #</p>
        </div>

        <div class="div-puntaje rounded p-3" >
            <p class="h3 text-center fw-bold">Puntos</p>
            <div v-if="showTeamFirst == 1" class="d-flex justify-content-around col-12">
                <div class="col-6">
                    <p class="points text-center">{{ puntosEquipo1 }}</p>
					<div class="d-flex justify-content-center">
						<button class="btn btn-primary" @click="puntoEquipo1"><i class="fa-solid fa-plus h1"></i></button>
					</div>
                </div>
                <div class="col-6">
                    <p class="points text-center">{{ puntosEquipo2 }}</p>
					<div class="d-flex justify-content-center">
						<button class="btn btn-primary" @click="puntoEquipo2"><i class="fa-solid fa-plus h1"></i></button>
					</div>                
				</div>
            </div>
			<div v-else class="d-flex justify-content-around col-12">
                <div class="col-6">
                    <p class="points text-center">{{ puntosEquipo2 }}</p>
					<div class="d-flex justify-content-center">
						<button class="btn btn-primary" @click="puntoEquipo2"><i class="fa-solid fa-plus h1"></i></button>
					</div>                
				</div>
				<div class="col-6">
                    <p class="points text-center">{{ puntosEquipo1 }}</p>
					<div class="d-flex justify-content-center">
						<button class="btn btn-primary" @click="puntoEquipo1"><i class="fa-solid fa-plus h1"></i></button>
					</div>
                </div>
            </div>
        </div>

		<div class="mt-4">
			<p class="h4 text-center fw-bold">Sets</p>
			<div v-if="showTeamFirst == 1" class="d-flex justify-content-around col-12">
                <div class="col-6">
                    <p class="sets text-center">{{ equipo1Sets }}</p>
					<p class="equipo text-center">{{ equipo1 }}</p>
                </div>
                <div class="col-6">
                    <p class="sets text-center">{{ equipo2Sets }}</p>
					<p class="equipo text-center">{{ equipo2 }}</p>
				</div>
            </div>

			<div v-else class="d-flex justify-content-around col-12">

                <div class="col-6">
                    <p class="sets text-center">{{ equipo2Sets }}</p>
					<p class="equipo text-center">{{ equipo2 }}</p>
				</div>
				<div class="col-6">
                    <p class="sets text-center">{{ equipo1Sets }}</p>
					<p class="equipo text-center">{{ equipo1 }}</p>
                </div>
            </div>
		</div>

		<div class="d-flex justify-content-center align-items-center mt-3">
			<button class="btn btn-secondary mx-4" @click="deshacerAccion"><i class="fa-solid fa-arrow-left h2 my-auto p-2"></i></button>
			<button class="btn btn-secondary mx-4" @click="showTeamSwitch"><i class="fa-solid fa-right-left h2 my-auto p-2"></i></button>
		</div>
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
			showTeamFirst: localStorage.getItem("showTeamFirst") || 1,
			equipo1Sets: localStorage.getItem("equipo1Sets") || 0,
			equipo2Sets: localStorage.getItem("equipo2Sets") || 0,
            acciones: [],

		};
	},
	methods: {
		puntoEquipo1() {
			this.puntosEquipo1++;
			// localStorage.setItem("puntosEquipo1", this.puntosEquipo1);
            this.acciones.push({ tipo: "suma", equipo: 1 });
            this.guardarPuntos();
			this.setWin();
		},
		puntoEquipo2() {
			this.puntosEquipo2++;
			// localStorage.setItem("puntosEquipo2", this.puntosEquipo2);
            this.acciones.push({ tipo: "suma", equipo: 2 });
            this.guardarPuntos();
			this.setWin();
		},
        deshacerAccion() {
            const ultimaAccion = this.acciones.pop();
            if (ultimaAccion) {
                if (ultimaAccion.tipo === "suma") {
                    if (ultimaAccion.equipo === 1) {
                        this.puntosEquipo1--;
                    } else {
                        this.puntosEquipo2--;
                    }
                    this.guardarPuntos();
                }
                // Puedes agregar más tipos de acciones aquí si lo necesitas
            }
        },
        guardarPuntos() {
            localStorage.setItem("puntosEquipo1", this.puntosEquipo1);
            localStorage.setItem("puntosEquipo2", this.puntosEquipo2);
        },
		showTeamSwitch() {
			this.showTeamFirst = this.showTeamFirst == 1 ? 2 : 1;
            localStorage.setItem("showTeamFirst", this.showTeamFirst); // Convertir a cadena
		},
		setWin(){
			if(this.puntosEquipo1 >= 11){
				this.equipo1Sets++;
				localStorage.setItem("equipo1Sets", this.equipo1Sets);
				this.puntosEquipo1 = 0;
				this.puntosEquipo2 = 0;
				localStorage.setItem("puntosEquipo1", this.puntosEquipo1);
				localStorage.setItem("puntosEquipo2", this.puntosEquipo2);
			}
			if(this.puntosEquipo2 >= 11){
				this.equipo2Sets++;
				localStorage.setItem("equipo2Sets", this.equipo2Sets);
				this.puntosEquipo1 = 0;
				this.puntosEquipo2 = 0;
				localStorage.setItem("puntosEquipo1", this.puntosEquipo1);
				localStorage.setItem("puntosEquipo2", this.puntosEquipo2);
			}	
		},
	},
};
</script>
