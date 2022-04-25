<template>
    <canvas class="hidden" ref="canvas" width="256" height="256"/>
    <template v-for="(grid, key) in chars">
        <Conway v-if="grid" class="conway" :mask="grid" :key="key"/>
        <span v-else class="space">&nbsp;</span>
    </template>
</template>

<script>
import Conway from './Conway.vue';

export default {
    components: {
        Conway
    },
    data() {
        return {
            grids: [],
            text: ''
        };
    },
    mounted() {
        this.text = this.getText(this.$slots.default());
        this.grids = this.calcGrid();
    },
    computed: {
        asArray() {
            return this.text.split("");
        },
        alphanum() {
            return this.asArray.filter(v => v !== ' ');
        },
        chars() {
            let key = 0;
            return this.asArray.map(char => {
                if (char === ' ') {
                    return null;
                }

                return this.grids[key++];
            });
        }
    },
    methods: {
        getText(slot) {
            if (typeof slot === 'string') {
                return slot;
            }

            if (Array.isArray(slot)) {
                return slot.map(nestedslot => this.getText(nestedslot)).flat(255).join('');
            }

            if (slot.children && typeof slot.children === 'string') {
                return slot.children;
            }

            if (slot.children && Array.isArray(slot.children)) {
                return slot.children.map(nestedslot => this.getText(nestedslot)).flat(255).join('');
            }
        },
        calcGrid() {
            return this.alphanum.map(char => this.toGrid(char));
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

            const style = window.getComputedStyle(this.$refs.canvas);
            const size = style.getPropertyValue('font-size');
            const family = style.getPropertyValue('font-family');

            ctx.fillStyle = '#000';
            ctx.font = `${size} ${family}`;

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
