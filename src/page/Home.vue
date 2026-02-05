<script setup>
import { ref, onMounted, computed } from 'vue';

// Refs
const form = ref({ id: null, nome: '', telefone: '', maiorIdade: false });
const lista = ref([]);
const termoBusca = ref(''); 

// Funções
function criarUsuario() {
  const validadorId = lista.value.findIndex(function (item) {
    return item.id === form.value.id;
  });

  if (validadorId !== -1) {
    lista.value[validadorId] = { ...form.value };
  } else {
    const novoUsuario = { ...form.value, id: Date.now() };
    lista.value.push(novoUsuario);
  }

  persistirDados();
  limparFormulario();
}

function editar(item) {
  form.value = { ...item };
}

function excluir(id) {
  lista.value = lista.value.filter(function (item) {
    return item.id !== id;
  });
  persistirDados();
}

// LocalStorage
function persistirDados() {
  localStorage.setItem('minhaLista', JSON.stringify(lista.value));
}

function limparFormulario() {
  form.value = { id: null, nome: '', telefone: '', maiorIdade: false };
}

// Carregar página
onMounted(function () {
  const salvo = localStorage.getItem('minhaLista');
  if (salvo) {
    lista.value = JSON.parse(salvo);
  }
});

// Filtro
const listaFiltrada = computed(function () {
  return lista.value.filter(function (item) {
    return item.nome.toLowerCase().includes(termoBusca.value.toLowerCase());
  });
});
</script>


<template>
  <form @submit.prevent="criarUsuario" class="formularioCadastro p-3 border rounded">
    <div class="mb-3">
      <label class="form-label">Nome:</label>
      <input v-model="form.nome" type="text" class="form-control">
    </div>
    <div class="mb-3">
      <label class="form-label">Telefone</label>
      <input v-model="form.telefone" type="text" class="form-control">
    </div>
    <div class="mb-3 form-check">
      <input v-model="form.maiorIdade" type="checkbox" class="form-check-input" id="inputMaiorIdade">
      <label class="form-check-label" for="inputMaiorIdade">Maior de idade</label>
    </div>

    <button type="submit" class="btn btn-primary">
      {{ form.id ? 'Salvar Alteração' : 'Adicionar' }}
    </button>
  </form>

  <nav class="navbar bg-body-tertiary mt-3">
    <div class="container-fluid">
      <input v-model="termoBusca" class="form-control" type="search" placeholder="Pesquisar por nome">
    </div>
  </nav>

  <table class="table mt-3">
    <thead>
      <tr>
        <th>Nome</th>
        <th>Telefone</th>
        <th>Maior idade</th>
        <th>Ações</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in listaFiltrada" :key="item.id">
        <td>{{ item.nome }}</td>
        <td>{{ item.telefone }}</td>
        <td>{{ item.maiorIdade ? 'Sim' : 'Não' }}</td>
        <td>
          <button @click="editar(item)" class="btn btn-sm btn-outline-primary me-2">Editar</button>
          <button @click="excluir(item.id)" class="btn btn-sm btn-outline-danger">Excluir</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>
