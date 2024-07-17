<template>
    <br><br>
    <form @submit.prevent="submitForm" class="container">
        <div class="form-group">
            <label for="nota1">NOTA 1:</label>
            <input type="number" id="nota1" v-model="form.nota1" @input="validateNota1" class="form-control" min="10" max="70"/>
            <p v-if="errors.nota1" class="error-message">{{ errors.nota1 }}</p>
        </div>
        <div class="form-group">
            <label for="nota2">NOTA 2:</label>
            <input type="number" id="nota2" v-model="form.nota2" @input="validateNota2" class="form-control" min="10" max="70"/>
            <p v-if="errors.nota2" class="error-message">{{ errors.nota2 }}</p>
        </div>
        <div class="form-group">
            <label for="nota3">NOTA 3:</label>
            <input type="number" id="nota3" v-model="form.nota3" @input="validateNota3" class="form-control" min="10" max="70"/>
            <p v-if="errors.nota3" class="error-message">{{ errors.nota3 }}</p>
        </div>
        <div class="form-group">
            <label for="attendance">Porcentaje de Asistencia:</label>
            <input type="number" id="attendance" v-model="form.attendance" @input="validateAttendance" class="form-control" min="0" max="100"/>
            <p v-if="errors.attendance" class="error-message">{{ errors.attendance }}</p>
        </div>
        <button type="submit" class="btn btn-primary">Calcular</button>
        <p v-if="resultMessage" class="result-message">{{ resultMessage }}</p>
    </form>
</template>

<script>
    export default {
        data() {
            return {
                form: {
                    nota1: null,
                    nota2: null,
                    nota3: null,
                    attendance: null
                },
                errors: {
                    nota1: null,
                    nota2: null,
                    nota3: null,
                    attendance: null
                },
				resultMessage: ''

            };
        },
        methods: {
             validateNota1() {
                if (this.form.nota1 === null) {
                    this.errors.nota1 = 'El campo NOTA 1 es requerido';
                } else if (this.form.nota1 < 10 || this.form.nota1 > 70) {
                    this.errors.nota1 = 'La NOTA 1 debe estar entre 10 y 70';
                } else {
                    this.errors.nota1 = '';
                }
            },
            validateNota2() {
                if (this.form.nota2 === null) {
                    this.errors.nota2 = 'El campo NOTA 2 es requerido';
                } else if (this.form.nota2 < 10 || this.form.nota2 > 70) {
                    this.errors.nota2 = 'La NOTA 2 debe estar entre 10 y 70';
                } else {
                    this.errors.nota2 = '';
                }
            },
            validateNota3() {
                if (this.form.nota3 === null) {
                    this.errors.nota3 = 'El campo NOTA 3 es requerido';
                } else if (this.form.nota3 < 10 || this.form.nota3 > 70) {
                    this.errors.nota3 = 'La NOTA 3 debe estar entre 10 y 70';
                } else {
                    this.errors.nota3 = '';
                }
            },
            validateAttendance() {
                if (this.form.attendance === null) {
                    this.errors.attendance = 'El campo porcentaje de asistencia es requerido';
                } else if (this.form.attendance < 0 || this.form.attendance > 100) {
                    this.errors.attendance = 'El porcentaje de asistencia debe estar entre 0 y 100';
                } else {
                    this.errors.attendance = '';
                }
            },
            submitForm() {
                this.validateNota1();
                this.validateNota2();
                this.validateNota3();
                this.validateAttendance();

			if (!Object.values(this.errors).some(error => error !== '')) {
			const finalGrade = (this.form.nota1 * 0.35) + (this.form.nota2 * 0.35) + (this.form.nota3 * 0.30);
			let resultMessage = '';

			if (finalGrade < 40) {
            resultMessage += 'Reprobado por notas. ';
			} else {
            resultMessage += 'Aprobado por notas. ';
			}

			if (this.form.attendance < 80) {
            resultMessage += 'Reprobado por porcentaje de asistencia.';
			} else {
            resultMessage += 'Aprobado por porcentaje de asistencia.';
			}

        this.resultMessage = resultMessage;
    }
            }
        }
    };
</script>

<style scoped>
    .container {
        width: 50%;
        margin: 0 auto;
        padding: 20px;
        border: 1px solid #ccc;
        border-radius: 5px;
    }

    .form-group {
        margin-bottom: 20px;
    }

    .label {
        font-weight: bold;
    }

    .form-control {
        width: 100%;
        padding: 10px;
        border: 1px solid #ccc;
        border-radius: 5px;
        box-sizing: border-box;
    }

    .error-message {
        color: red;
        margin-top: 5px;
    }

    .btn-primary {
        background-color: #007bff;
        color: #fff;
        padding: 10px 20px;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }

    /* Estilos adicionales para mejorar la apariencia */
    form {
        display: flex;
        flex-direction: column;
    }

    label {
        margin-bottom: 5px;
    }

    input[type="text"],
    input[type="password"],
    input[type="email"] {
        margin-bottom: 10px;
    }

    button {
        margin-top: 20px;
    }

</style>
