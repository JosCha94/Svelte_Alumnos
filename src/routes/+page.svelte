<script>
  import { json } from "@sveltejs/kit";
  import "bootstrap/dist/css/bootstrap.min.css";
  import "bootstrap/dist/js/bootstrap.min.js";

  /**
   * @type {any[]}
   */
  let empleados = [];
  let datosEmpleado = {
    id: null,
    nombre: "",
    correo: "",
  };

  let mostrarEmpleados = () => {
    fetch("http://localhost/API%20Empleados/")
      .then((respuesta) => respuesta.json())
      .then((datosRespuesta) => {
        empleados = datosRespuesta;

        datosRespuesta = {
          id: null,
          nombre: "",
          correo: "",
        };
        console.log(empleados);
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
              <label for="Nombre" class="form-label">Nombre</label>
              <input type="text" class="form-control" id="Nombre" />
            </div>
            <div class="mb-3">
              <label for="Correo" class="form-label">Correo</label>
              <input type="email" class="form-control" id="Correo" />
            </div>

            <button type="button" class="btn btn-primary"
              >Agregar Empleado</button
            >
            <button type="button" class="btn btn-primary"
              >Actualizar Empleado</button
            >
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
              <td><button class="btn btn-warning" type="submit">Editar</button> | <button class="btn btn-danger" type="submit">Borrar</button></td>
            </tr>
          {/each}
        </tbody>
      </table>
    </div>
  </div>
</div>
