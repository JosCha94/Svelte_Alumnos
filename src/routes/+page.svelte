<script>
  import "bootstrap/dist/css/bootstrap.min.css";
  import "bootstrap/dist/js/bootstrap.min.js";

  
</script>

<div class="container my-3">
    <div class="row gap-xs-3">
        <h1 class="text-center mb-4">API DE EMPLEADOS <span class="h3"> con svelte</span></h1>
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
  
            <button type="button" class="btn btn-primary">Agregar Empleado</button>
            <button type="button" class="btn btn-primary">Actualizar Empleado</button>
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
        <tr>
          <th>1</th>
          <td>Mark</td>
          <td>Otto</td>
          <td>@mdo</td>
        </tr>
        <tr>
          <th>2</th>
          <td>Jacob</td>
          <td>Thornton</td>
          <td>@fat</td>
        </tr>
        <tr>
          <th>3</th>
          <td>Larry the Bird</td>
          <td>@twitter</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>
</div>
