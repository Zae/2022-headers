<template>
    <canvas ref="canvas" :width="width" :height="height"/>
</template>

<script>
export default {
    props: {
        mask: {
            type: Array,
            required: true
        }
    },
    data() {
        return {
            grid: [],
            current: 0
        };
    },
    computed: {
        height() {
            return this?.mask?.length ?? 0;
        },
        width() {
            return this?.mask?.[0]?.length ?? 0;
        },
        ctx() {
            return this.$refs?.canvas?.getContext('2d') ?? null;
        },
        next() {
            return this.current === 1 ? 0 : 1;
        }
    },
    mounted() {
        this.setup();
        window.requestAnimationFrame(this.loop);
    },
    methods: {
        loop() {
            // calculate
            this.run();

            // loop!
            window.requestAnimationFrame(this.loop);
        },
        setup() {
            this.grid[0] = this.createGrid(this.height, this.width);
            this.grid[1] = this.createGrid(this.height, this.width);

            for (const y in this.grid[0]) {
                for (const x in this.grid[0][y]) {
                    if (this.mask[y][x]) {
                        this.grid[0][y][x] = Math.round(Math.random());
                    }
                }
            }
        },
        run() {
            for (let y = 0; y < this.grid[this.current].length; y++) {
                for (let x = 0; x < this.grid[this.current][y].length; x++) {
                    if (this.mask[y][x]) {
                        const n = this.neighbours(y, x);

                        if (this.grid[this.current][y][x]) {
                            if (n < 2 || n > 3) {
                                this.grid[this.next][y][x] = 0;
                                this.ctx.clearRect(x, y, 1, 1);
                            } else {
                                this.grid[this.next][y][x] = 1;
                                this.ctx.fillRect(x, y, 1, 1);
                            }
                        } else {
                            if (n === 3) {
                                this.grid[this.next][y][x] = 1;
                                this.ctx.fillRect(x, y, 1, 1);
                            } else {
                                this.grid[this.next][y][x] = 0;
                                this.ctx.clearRect(x, y, 1, 1);
                            }
                        }
                    } else {
                        this.grid[this.next][y][x] = 0;
                        this.ctx.clearRect(x, y, 1, 1);
                    }
                }
            }

            this.current = this.current === 1 ? 0 : 1;
        },
        neighbours(y, x) {
            return (this.grid[this.current]?.[y - 1]?.[x - 1] ?? 0) +
                (this.grid[this.current]?.[y]?.[x - 1] ?? 0) +
                (this.grid[this.current]?.[y + 1]?.[x - 1] ?? 0) +
                (this.grid[this.current]?.[y - 1]?.[x] ?? 0) +
                (this.grid[this.current]?.[y + 1]?.[x] ?? 0) +
                (this.grid[this.current]?.[y - 1]?.[x + 1] ?? 0) +
                (this.grid[this.current]?.[y]?.[x + 1] ?? 0) +
                (this.grid[this.current]?.[y + 1]?.[x + 1] ?? 0);
        },
        createGrid(h, w) {
            const grid = new Array(h);
            grid.fill([]);

            return grid.map(() => {
                const row = new Array(w);
                row.fill(0);
                return row;
            });
        }
    }
}
</script>

<style scoped>
div {
    display: block;
    width: calc(v-bind(width) * 1px);
    height: calc(v-bind(height) * 1px);
}
</style>
