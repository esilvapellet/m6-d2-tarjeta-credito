<template>
  <div class="contenedorTarjeta">
    <div class="row">
      <div class="col-12 col-md-6">
        <form action="#">
          <p class="py-2 fw-bold">• Tipo de tarjeta</p>
          <hr />
          <div class="form-floating py-2">
            <select
              class="form-select"
              id="selectTipo"
              aria-label="Floating label select example"
              v-model="tarjeta.tituloTarjeta"
              @change="cambiarTarjeta(tarjeta.tituloTarjeta)"
            >
              <option value="" selected>Seleccionar...</option>
              <option value="American Express">American Express</option>
              <option value="MasterCard">MasterCard</option>
              <option value="Visa">Visa</option>
            </select>
            <label for="selectTipo">Seleccione tipo de tarjeta</label>
          </div>

          <div class="form-floating mb-3">
            <input
              type="text"
              class="form-control"
              id="tipoTar"
              placeholder=" "
              :value="tarjeta.tituloTarjeta"
              disabled
            />
            <label for="tipoTar">Tipo de Tarjeta</label>
          </div>

          <div>
            <p class="py-2 fw-bold">• Tecnología de tarjeta</p>
            <hr />
            <div class="form-check py-2">
              <input
                class="form-check-input"
                type="radio"
                name="tipoTarjeta"
                id="contactLess"
                v-model="tarjeta.chipTarjeta"
                :value="true"
                checked
              />
              <label class="form-check-label" for="contactLess">
                Contact Less
              </label>
            </div>
            <div class="form-check">
              <input
                class="form-check-input"
                type="radio"
                name="tipoTarjeta"
                id="bandaMagnetica"
                v-model="tarjeta.chipTarjeta"
                :value="false"
              />
              <label class="form-check-label" for="bandaMagnetica">
                Banda Magnética
              </label>
            </div>
          </div>
          <p class="py-2 fw-bold">• Datos Cliente</p>
          <hr />
          <div class="form-floating mb-3">
            <input
              type="text"
              class="form-control"
              id="nombreTar"
              placeholder=""
              value=""
              v-model="tarjeta.nomTarjeta"
            />
            <label for="nombreTar">Nombre cliente</label>
          </div>
          <div class="col-12">
            <button
              id="generaCard"
              class="btn btn-success py-2 w-100"
              @click="generarNumero()"
            >
              Generar Datos de Tarjeta
            </button>
          </div>
          <p class="py-2 fw-bold">• Datos Tarjeta</p>
          <hr />
          <div class="form-floating py-2">
            <input
              type="text"
              class="form-control"
              id="numeroTar"
              placeholder=" "
              value=" "
              v-model="tarjeta.numTarjeta"
            />
            <label for="numeroTar">Número tarjeta (12 dígitos)</label>
          </div>
          <div class="form-floating py-2">
            <input
              type="text"
              class="form-control"
              id="expTarjeta"
              placeholder=""
              value=""
              v-model="tarjeta.fechaExp"
            />
            <label for="expTarjeta">Fecha expiración (mes/año)</label>
          </div>
        </form>
      </div>
      <div class="col-12 col-md-6" id="vistaTarjeta">
        <div class="tarjeta">
          <span>{{ tarjeta.tituloTarjeta }}</span>
          <img
            width="40"
            src="./assets/img/chip.jpg"
            v-if="tarjeta.chipTarjeta"
          />
          <!-- <img
            width="40"
            :src="tarjeta.chipTarjeta"
            v-if="tarjeta.chipTarjeta"
          /> -->
          <div class="cajaChip" v-if="!tarjeta.chipTarjeta"></div>
          <div>
            <h2>{{ tarjeta.numTarjeta }}</h2>
            <span
              >Fecha Exp:
              <b class="vencimiento">{{ tarjeta.fechaExp }}</b></span
            >
          </div>
          <footer>
            <span>{{ tarjeta.nomTarjeta }}</span>
            <img :src="tarjeta.currentTarget" height="35px" max-width="60" />
          </footer>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import moment from "moment";
export default {
  name: "CardTarjeta",
  data() {
    return {
      tarjeta: {
        tituloTarjeta: "",
        chipTarjeta: true,
        currentTarget: "",
        numTarjeta: " ",
        fechaExp: " ",
        nomTarjeta: " ",
        tipoTarjeta: [
          {
            id: 1,
            path: "./assets/img/american.png",
            texto: "American Express",
          },
          { id: 2, path: "./assets/img/mastercard.png", texto: "MasterCard" },
          { id: 3, path: "./assets/img/visa2.png", texto: "Visa" },
        ],
      },
    };
  },

  methods: {
    cambiarTarjeta: function (nomTarjeta) {
      if (nomTarjeta == "American Express") {
        this.tarjeta.currentTarget = this.tarjeta.tipoTarjeta[0].path;
        console.log(this.tarjeta.currentTarget);
        console.log(this.tarjeta.tipoTarjeta);
      } else if (nomTarjeta == "MasterCard") {
        this.tarjeta.currentTarget = this.tarjeta.tipoTarjeta[1].path;
      } else if (nomTarjeta == "Visa") {
        this.tarjeta.currentTarget = this.tarjeta.tipoTarjeta[2].path;
      } else {
        this.tarjeta.currentTarget = false;
      }
    },
    generarNumero: function () {
      event.preventDefault();
      this.tarjeta.numTarjeta = Math.floor(
        Math.random() * (599999999999 - 300000000000) + 300000000000
      );
      let fechaVenc = moment().add(5, "year");
      this.tarjeta.fechaExp = fechaVenc.format("MM/YY");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  margin: 0;
}
.contenedorTarjeta {
  display: flex;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  /* height: 95vh; */
  font-size: 12px;
  font-family: sans-serif;
  gap: 40px;
  background: rgb(0, 0, 0, 0.5);
}

form {
  padding: 10px;
  border-radius: 20px;
  /* border: ridge 1px; */
  /* box-shadow: 0px 0px 10px 2px black; */
  /* font-weight: bold; */
  /* display: flex; */
  flex-direction: column;
  gap: 10px;
  justify-content: center;
  /* background-color: black; */
  background-color: rgb(0, 0, 0, 0.75);
  color: white;
  border-color: none;
}
form div {
  /* display: grid; */
  /* grid-template-columns: 100px 200px; */
  align-items: center;
  gap: 5px;
}

form div label {
  text-align: right;
}

.tarjeta {
  width: 400px;
  height: 250px;
  background: #1c1a1e;
  color: white;
  border-radius: 20px;
  padding: 20px;
  box-shadow: 0px 0px 10px 2px black;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

h3 {
  font-size: 20px;
}

h2,
.vencimiento,
#expTarjeta,
#numeroTar {
  font-family: monospace;
}

h2 {
  font-size: 30px;
  letter-spacing: 8px;
  margin-bottom: 15px;
  text-shadow: 0px 0px 1px gold;
  text-align: center;
}

b {
  font-size: 16px;
}

footer {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  font-weight: bold;
  font-size: 18px;
  text-transform: uppercase;
  font-style: italic;
}

.cajaChip {
  width: 100%;
  height: 35.148px;
  background: rgb(128, 128, 128);
  background: linear-gradient(
    72deg,
    rgba(128, 128, 128, 1) 0%,
    rgba(113, 113, 113, 1) 22%,
    rgba(208, 208, 208, 1) 100%
  );
}

#vistaTarjeta {
  align-content: center;
}
</style>
