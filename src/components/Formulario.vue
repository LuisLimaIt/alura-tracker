<template>
    <div class="box formulario">
        <div class="columns">
            <div class="column is-5" role="form" aria-label="Formulário para criação de uma nova tarefa">
                <input type="text" class="input" placeholder="Qual tarefa você deseja iniciar?" v-model="descricao" />
            </div>
            <div class="column is-3">
                <div class="select">
                    <select v-model="idProjeto">
                        <option value="">Selecione o projeto</option>
                        <option :value="projeto.id" v-for="projeto in projetos" :key="projeto.id">
                            {{ projeto.name }}
                        </option>
                    </select>
                </div>
            </div>
            <div class="column">
                <TemporizadorVue @aoTemporizadorFinalizado="finalizarTarefa" />
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { computed, defineComponent } from 'vue';
import TemporizadorVue from './Temporizador.vue';
import { useStore } from '@/store';
// import { NOTIFICAR } from '@/store/tipo-mutacoes';
// import { TipoNotificacao } from '@/interfaces/INotificacao';


export default defineComponent({
    name: 'FormularioVue',
    emits: ['aoSalvarTarefa'],
    components: {
        TemporizadorVue
    },
    data() {
        return {
            descricao: '',
            idProjeto: ''
        }
    },
    methods: {
        finalizarTarefa(tempoDecorrido: number): void {

            // if (!this.projetos.find((p) => p.id == this.idProjeto)) {
            //     this.store.commit(NOTIFICAR, {
            //         titulo: 'A tarefa não foi salva!',
            //         texto: "Selecione um projeto antes de finalizar!",
            //         tipo: TipoNotificacao.FALHA,
            //     }); 
            //     return; 
            // }

            this.$emit('aoSalvarTarefa', {
                duracaoEmSegundos: tempoDecorrido,
                descricao: this.descricao,
                projeto: this.projetos.find(proj => proj.id == this.idProjeto)
            })
            this.descricao = '';
        }
    },
    setup() {
        const store = useStore()
        return {
            projetos: computed(() => store.state.projetos),
            store
        }
    }
});
</script>

<style>
.formulario {
    color: var(--texto-primario);
    background: var(--bg-primario);
}
</style>