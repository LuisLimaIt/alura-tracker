<template>
  <main class="columns is-gapless is-multiline">
    <div class="column is-one-quarter">
      <BarraLateral />
    </div>
    <div class="column is-three-quarter">
      <FormularioVue @aoSalvarTarefa="salvarTarefa"/>
      <div class="lista">
        <TarefaVue v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" />
        <BoxVue v-if="listaEstaVazia">
          Você ainda não iniciou nenhuma tarefa hoje! :P 
        </BoxVue>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import FormularioVue from './components/Formulario.vue';
import TarefaVue from './components/Tarefa.vue';
import ITarefa from './interfaces/ITarefa';
import BoxVue from './components/Box.vue';

export default defineComponent({
  name: 'App',
  components: {
    BarraLateral,
    FormularioVue,
    TarefaVue,
    BoxVue
  },
  data() {
    return {
      tarefas: [] as ITarefa[]
    }
  },
  computed: {
    listaEstaVazia() : boolean {
      return this.tarefas.length === 0;
    }
  },
  methods: {
    salvarTarefa (tarefa: ITarefa) {
      this.tarefas.push(tarefa);
    }
  }
});
</script>

<style>
  .lista {
    padding: 1.25rem;
  }
</style>
