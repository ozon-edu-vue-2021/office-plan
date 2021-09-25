<template>
    <div class="map">
        <h3>Карта офиса</h3>

        <div class="map-root">
            <MapSVG />
        </div>
    </div>
</template>

<script>
import MapSVG from '@/assets/map.svg';

export default {
    components: {
        MapSVG,
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
