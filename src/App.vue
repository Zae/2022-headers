<template>
    <div class="first">
        <h1><HeaderAutomata>Lorem <span>ipsum</span></HeaderAutomata></h1>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Euismod in pellentesque massa placerat duis ultricies. Odio morbi quis commodo odio aenean sed adipiscing diam donec. Nullam eget felis eget nunc. Mollis aliquam ut porttitor leo a. Sit amet dictum sit amet justo donec. </p>
    </div>
    <div class="second">
        <h1><HeaderAutomata>Lorem ipsum</HeaderAutomata></h1>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Euismod in pellentesque massa placerat duis ultricies. Odio morbi quis commodo odio aenean sed adipiscing diam donec. Nullam eget felis eget nunc. Mollis aliquam ut porttitor leo a. Sit amet dictum sit amet justo donec. </p>
    </div>
    <div class="third">
        <h1><HeaderAutomata>Lorem ipsum</HeaderAutomata></h1>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Euismod in pellentesque massa placerat duis ultricies. Odio morbi quis commodo odio aenean sed adipiscing diam donec. Nullam eget felis eget nunc. Mollis aliquam ut porttitor leo a. Sit amet dictum sit amet justo donec. </p>
    </div>
    <div class="fourth">
        <h1><HeaderAutomata>Lorem ipsum</HeaderAutomata></h1>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Euismod in pellentesque massa placerat duis ultricies. Odio morbi quis commodo odio aenean sed adipiscing diam donec. Nullam eget felis eget nunc. Mollis aliquam ut porttitor leo a. Sit amet dictum sit amet justo donec. </p>
    </div>
    <div class="fifth">
        <h1><HeaderAutomata>Lorem ipsum</HeaderAutomata></h1>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Euismod in pellentesque massa placerat duis ultricies. Odio morbi quis commodo odio aenean sed adipiscing diam donec. Nullam eget felis eget nunc. Mollis aliquam ut porttitor leo a. Sit amet dictum sit amet justo donec. </p>
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
h1 { font-size: 6em; }

.first, .second, .third, .fourth, .fifth {
    font-size: 2em;
    line-height: 1;
}

.first { font-family: Helvetica, serif; }
.second { font-family: "Times New Roman", serif; }
.third { font-family: 'Noto Serif Display', serif; }
.fourth { font-family: 'Square Peg', cursive; }
.fifth { font-family: 'Tapestry', cursive; }

h1, h2, h3, h4, h5, p {
    margin: 10px 0;
}
</style>
