<template>
    <canvas class="hidden" ref="canvas" width="1024" height="1024"/>
    <Conway class="conway" v-for="(grid, key) in grids" :mask="grid" :key="key"/>
</template>

<script>
import Conway from './Conway.vue';

export default {
    components: {
        Conway
    },
    props: {
        text: {
            type: String,
            default: 'Conway'
        }
    },
    data() {
        return {
            grids: []
        };
    },
    mounted() {
        this.grids = this.calcGrid();
    },
    computed: {
        asArray() {
            return this.text.split("").filter(v => v !== ' ');
        }
    },
    methods: {
        calcGrid() {
            return this.asArray.map(char => this.toGrid(char));
        },
        createGrid(h, w) {
            const grid = new Array(h);
            grid.fill([]);

            return grid.map(() => {
                const row = new Array(w);
                row.fill(false);
                return row;
            });
        },
        toGrid(char) {
            const ctx = this.$refs.canvas.getContext('2d');
            ctx.clearRect(0, 0, 1024, 1024);

            ctx.fillStyle = '#000';
            ctx.font = '25em serif';

            const txtMetrics = ctx.measureText(char);

            const width = Math.ceil(Math.abs(txtMetrics.actualBoundingBoxLeft) + Math.abs(txtMetrics.actualBoundingBoxRight));
            const height = Math.ceil(txtMetrics.actualBoundingBoxAscent + txtMetrics.actualBoundingBoxDescent);
            ctx.fillText(char, 0, height);

            const bitmap = ctx.getImageData(0, 0, width, height);
            const grid = this.createGrid(height, width);

            for (let i = 3; i < bitmap.data.length; i += 4) {
                const pixel = Math.floor(i / 4);
                const y = Math.floor(pixel / width);
                const x = pixel % width;

                grid[y][x] = !!(bitmap.data[i]);
            }

            return grid;
        }
    }
}
</script>

<style scoped>
canvas.hidden {
    position: absolute;
    top: 0;
    left: 0;
    display: none;
}

.conway {
    display: inline-block;
}
</style>
