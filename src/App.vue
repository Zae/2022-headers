<template>
    <div class="third">
        <h1>
            <HeaderAutomata>CREATIVE</HeaderAutomata> <br/>
            <HeaderAutomata>CODING</HeaderAutomata>
        </h1>
    </div>
</template>

<script>
import HeaderAutomata from './components/HeaderAutomata.vue';

export default {
    components: {
        HeaderAutomata
    }
}
</script>

<style>
h1 { font-size: 9em; }

.third {
    font-size: 2em;
    line-height: 1;
}

h1, h2, h3, h4, h5, p {
    margin: 10px 10px;
}
</style>
