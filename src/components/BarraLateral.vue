<template>
    <header>
        <h1>
            <img src="../assets/logo.png" alt="Logo Alura Tracker">
        </h1>
        <button class="button" @click="alterarTema">
            <i :class="textoBotao.icon"></i>
            <span class="textButton">{{ textoBotao.text }}</span>
        </button>
        <nav class="panel mt-5">
            <ul>
                <li>
                    <router-link to="/" class="link">
                        <i class="fas fa-tasks"></i>
                        Tarefas
                    </router-link>  
                </li>
                <li>
                    <router-link to="/projetos" class="link">
                        <i class="fas fa-project-diagram"></i>
                        Projetos
                    </router-link>  
                </li>
            </ul>
        </nav>
    </header>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'barraLateral',
    emits: ['aoTemaAlterado'],
    data() {
        return {
            modoEscuroAtivo: false
        }
    },
    computed: {
        textoBotao() {
            if(!this.modoEscuroAtivo) {
                return {text: 'Modo escuro',
                        icon: 'fa-regular fa-moon'}
            } else {
                return {text: 'Modo claro', icon: 'fa-regular fa-sun'}
            }
        }
    },
    methods: {
        alterarTema() {
            this.modoEscuroAtivo = !this.modoEscuroAtivo;
            this.$emit('aoTemaAlterado', this.modoEscuroAtivo);
        }
    }
});
</script>

<style scoped>
header {
    padding: 1rem;
    background: #0d3b66;
    width: 100%;
    height: 100vh;
    text-align: center;
}

.textButton {
    margin: 0 5px;
    font-weight: 600;
}

@media only screen and (max-width: 768px) {
    header {
        padding: 2.5rem;
        height: auto;
    }
}

.panel li {
    margin: 8px 0;
    text-align: start;
}
.link {
    color: #fff;
}
.link:hover {
    color: #faf0ca;
}
.link.router-link-active {
    color: #faf0ca;
}

</style>