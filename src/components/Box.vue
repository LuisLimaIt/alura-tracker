<template>
    <div class="box has-text-weight-bold" :style="estilos">
        <slot />
    </div>
</template>

<script lang="ts">
    import { defineComponent } from 'vue';

    export default defineComponent({
        name: 'BoxVue',
        data() {
            return {
               estilos: {
                    backgroundColor: '#FAF0CA'
               }
            }
        }
    });

</script>