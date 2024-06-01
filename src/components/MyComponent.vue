<!-- src/components/MyComponent.vue -->
<template>
    <div>
        <Button label="Warning" severity="warning" />
    </div>
    
    <i class="pi pi-spin pi-stop" style="font-size: 2rem"></i>
    <i class="pi pi-spin pi-cog" style="font-size: 2rem"></i>

</template>

<script>
import { defineComponent } from 'vue';
import Button from 'primevue/button';

import 'primevue/resources/themes/mdc-dark-indigo/theme.css';
import 'primeicons/primeicons.css'


export default defineComponent({
components: {
    Button
}
});
</script>

<style>
</style>
  