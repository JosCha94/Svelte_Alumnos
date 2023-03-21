<script>
  // @ts-nocheck

  import { json } from "@sveltejs/kit";
  import "bootstrap/dist/css/bootstrap.min.css";
  import "bootstrap/dist/js/bootstrap.min.js";

  /**
   * @type {any[]}
   */
  let empleados = [];
  let activado = true;
  let datosEmpleado = {
    id: null,
    nombre: "",
    correo: "",
  };

  // MOSTRAR
  let mostrarEmpleados = () => {
    fetch("http://localhost/API%20Empleados%20con%20PHP/") 
      .then((respuesta) => respuesta.json())
      .then((datosRespuesta) => {
        empleados = datosRespuesta;

        datosEmpleado = {
          id: null,
          nombre: "",
          correo: "",
        };
        activado=true;
        //  console.log(empleados); //PARA VER LOS DATOS Q TRAE
         console.log(empleados);
      })
      .catch(console.log);
  };

  // AGREGAR
  let agregarEmpleado = () => {
    const nuevoEmpleado = {
      id: datosEmpleado.id,
      nombre: datosEmpleado.nombre,
      correo: datosEmpleado.correo,
    };

    fetch("http://localhost/API%20Empleados%20con%20PHP/?insertar=1", {
      method: "POST",
      body: JSON.stringify(nuevoEmpleado),
    })
      .then((respuesta) => respuesta.json())
      .then((datosRespuesta) => {
        // console.log(datosRespuesta) // PARA VER SI HAY ERRORES
        mostrarEmpleados();
      })
      .catch(console.log);
  };

  // BORRAR
  let borrarEmpleado = (id) => {
    fetch("http://localhost/API%20Empleados%20con%20PHP/?borrar=" + id)
      .then((respuesta) => respuesta.json())
      .then((datosRespuesta) => {
        mostrarEmpleados();
      })
      .catch(console.log);
  };

  // EDITAR
  let editarEmpleado = (empleado) => {
    datosEmpleado = empleado;
    activado = false;
  };

  // ACTUALIZAR
  let actualizarEmpleado = () => {
    fetch("http://localhost/API%20Empleados%20con%20PHP/?actualizar=" + datosEmpleado.id, {
      method: "POST",
      body: JSON.stringify(datosEmpleado),
    })
      .then((respuesta) => respuesta.json())
      .then((datosRespuesta) => {
        // console.log(datosRespuesta) PARA VER SI HAY ERRORES
        mostrarEmpleados();
        activado = true;
      })
      .catch(console.log);
  };

  mostrarEmpleados();
</script>

<div class="container my-3">
  <div class="row gap-xs-3">
    <h1 class="text-center mb-4">
      API DE EMPLEADOS <span class="h3"> con svelte</span>
    </h1>
    <div class="col-12 col-sm-6">
      <div class="card">
        <div class="card-header">Empleados</div>
        <div class="card-body">
          <form>
            <div class="mb-3">
              <label for="ID" class="form-label">ID</label>
              <input
                type="text"
                bind:value={datosEmpleado.id}
                class="form-control"
                id="ID"
                readonly
              />
              <div class="mb-3">
                <label for="Nombre" class="form-label">Nombre</label>
                <input
                  type="text"
                  bind:value={datosEmpleado.nombre}
                  class="form-control"
                  id="Nombre"
                />
              </div>
              <div class="mb-3">
                <label for="Correo" class="form-label">Correo</label>
                <input
                  type="email"
                  bind:value={datosEmpleado.correo}
                  class="form-control"
                  id="Correo"
                />
              </div>

              <button
                type="button"
                class="btn btn-primary"
                on:click|preventDefault={agregarEmpleado}
                disabled={!activado}
                >Agregar Empleado</button
              >
              <button
                type="button"
                class="btn btn-primary"
                on:click|preventDefault={actualizarEmpleado}
                disabled={activado}>Actualizar Empleado</button
              >
              <button
                type="button"
                class="btn btn-danger"
                on:click|preventDefault={mostrarEmpleados}>Cancelar</button
              >
            </div>
          </form>
        </div>
      </div>
    </div>
    <div class="col-12 col-sm-6">
      <table class="table">
        <thead>
          <tr>
            <th scope="col">ID</th>
            <th scope="col">Nombre</th>
            <th scope="col">Correo</th>
            <th scope="col">Acciones</th>
          </tr>
        </thead>
        <tbody>
          {#each empleados as empleado}
            <tr>
              <th>{empleado.id}</th>
              <td>{empleado.nombre}</td>
              <td>{empleado.correo}</td>
              <td
                ><button
                  class="btn btn-warning"
                  type="submit"
                  on:click={editarEmpleado(empleado)}>Editar</button
                >
                |
                <button
                  class="btn btn-danger"
                  type="submit"
                  on:click={borrarEmpleado(empleado.id)}>Borrar</button
                ></td
              >
            </tr>
          {/each}
        </tbody>
      </table>
    </div>
  </div>
</div>
