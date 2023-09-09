<template>
  <div id="deckgl-map"></div>
</template>

<script>
import { Deck } from '@deck.gl/core';
import { ScatterplotLayer } from '@deck.gl/layers';

export default {
  mounted() {
    this.initializeMap();
  },
  methods: {
    initializeMap() {
      const deckgl = new Deck({
        canvas: 'deckgl-map',
        initialViewState: {
          latitude: 37.7749,
          longitude: -122.4194,
          zoom: 12,
          bearing: 0,
          pitch: 0,
        },
        controller: true,
        layers: [
          new ScatterplotLayer({
            id: 'scatterplot-layer',
            data: [
              { position: [-122.4194, 37.7749], color: [255, 0, 0] },
              { position: [-122.408, 37.783], color: [0, 255, 0] },
              // Add more data points as needed
            ],
            getPosition: (d) => d.position,
            getRadius: 100,
            getColor: (d) => d.color,
          }),
        ],
      });

      deckgl.setProps({ layers: [scatterplotLayer] });
    },
  },
};
</script>

<style>
#deckgl-map {
  width: 100%;
  height: 400px;
}
</style>
