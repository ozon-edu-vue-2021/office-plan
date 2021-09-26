<template>
    <div class="map">
        <h3>Карта офиса</h3>

        <div
            v-if="!isLoading"
            class="map-root"
        >
            <MapSVG ref="svg" />
            <Table
                v-show="false"
                ref="table"
            />
        </div>
        <div v-else>Loading...</div>
    </div>
</template>

<script>
import * as d3 from 'd3';

import MapSVG from '@/assets/map.svg';
import Table from '@/assets/workPlace.svg';

import tables from "@/assets/tables.json";

export default {
    components: {
        MapSVG,
        Table
    },
    data() {
        return {
            isLoading: false,
            svg: null,
            g: null,
            tableSVG: null,
            tables: []
        }
    },
    created () {
        this.tables = tables;
    },
    mounted () {
        this.isLoading = false;

        this.svg = d3.select(this.$refs.svg);
        this.g = this.svg.select('g');
        this.tableSVG = d3.select(this.$refs.table);
        if (this.g) {
            this.drawTables();
        } else {
            alert('SVG is incorrect')
        }

        this.isLoading = false;
    },
    methods: {
        drawTables() {
            // создаем группу для рабочик мест
            const svgTablesGroupPlace = this.g // ??? почему пустой g пропадает в браузере
                .append('g')
                .attr('x', 0)
                .attr('y', 0)
                .classed('groupPlaces', true);

            this.tables.map(table => {
                // создает группу для рабочего стола
                const targetSeat = svgTablesGroupPlace
                    .append('g')
                    .attr('transform', `translate(${table.x}, ${table.y}) scale(0.5)`) // ??? почему недостаточно x y
                    .attr('x', `${table.x}`)
                    .attr('y', `${table.y}`)
                    .attr('id', `place_${table._id}`)
                    .classed('employer-place', true);

                // устанавливает стол в группу
                targetSeat
                    .append('g')
                    .attr(
                        'transform',
                        `rotate(${table.rotate || 0})`
                    )
                    .classed('table', true)
                    .html(this.tableSVG.html())
                    .style('fill', table.color ?? 'transparent')
                    .attr('width', '50px')
                    .attr('height', '50px');
            });
        }
    },
};
</script>

<style scoped>
.map {
    height: 100%;
    width: 100%;
    padding: 24px;
    overflow: hidden;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
}

.map-root {
    height: 100%;
    width: 100%;
    overflow: hidden;
    box-sizing: border-box;
}

h3 {
    margin-top: 0px;
}

>>> svg {
    height: 100%;
    width: 100%;
}
</style>
