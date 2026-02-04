<script>


</script>
<template>
  <form class="formularioCadastro">
    <div class="mb-3">
      <label class="form-label">Nome:</label>
      <input type="text" class="form-control" id="inputNome">
    </div>
    <div class="mb-3">
      <label class="form-label">Telefone</label>
      <input type="number" class="form-control" id="inputTelefone">
    </div>
    <div class="mb-3 form-check"> 
      <label class="form-check-label" >Se for maior de idade marque a caixa</label>
      <input type="checkbox" class="form-check-input" id="inputMaiorIdade">
    </div>
    <button type="submit" class="btn btn-primary">Adicionar</button>
  </form>
  <nav class="navbar bg-body-tertiary">
    <div class="container-fluid">
      <a class="navbar-brand">Pesquisar por</a>
      <form class="d-flex" role="search">
        <input v-model="nome" class="form-control me-2" type="search" placeholder="Nome" aria-label="Nome" />
        <input v-model="cpf" class="form-control me-2" type="search" placeholder="CPF" aria-label="Cpf" />
        <button class="btn btn-outline-success" type="submit">Search</button>
      </form>
    </div>
  </nav>
  <table class="table">
    <thead>
      <tr>
        <th scope="col">#</th>
        <th scope="col">Nome</th>
        <th scope="col">Telefone</th>
        <th scope="col">Maior idade</th>
        <th scope="col">Editar</th>
        <th scope="col">Excluir</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th scope="row">1</th>
        <td>Mark</td>
        <td>Otto</td>
        <td>@mdo</td>
        <td><button>Editar</button></td>
        <td><button>Excluir</button></td>
      </tr>
      <tr>
        <th scope="row">2</th>
        <td>Jacob</td>
        <td>Thornton</td>
        <td>@fat</td>
        <td><button>Editar</button></td>
        <td><button>Excluir</button></td>
      </tr>
      <tr>
        <th scope="row">3</th>
        <td>John</td>
        <td>Doe</td>
        <td>@social</td>
        <td><button>Editar</button></td>
        <td><button>Excluir</button></td>
      </tr>
    </tbody>
  </table>
</template>
