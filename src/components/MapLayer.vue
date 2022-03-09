 <template>
  <div>
      <div id="map" class="map"></div>
  </div>
</template>

<script>
import 'ol/ol.css';
import Map from 'ol/Map';
import OSM from 'ol/source/OSM';
import TileLayer from 'ol/layer/Tile';
import TileWMS from 'ol/source/TileWMS';
import View from 'ol/View';

export default {
   
    name: 'MapLayer',
    data() {
        return {
            zoom: 4,
            center: [0, 0],
            baseURL: 'https://ahocevar.com/geoserver/wms',
            layer: 'topp:states',
            projection: 'EPSG:3857',
            crossOrigin: 'anonymous',
            ratio: 1,
            serverType: 'geoserver',
        }
    },
    mounted() {
        this.map = new Map({
            target: 'map',
            layers: [
                new TileLayer({
                    source: new OSM()
                })
            ],
            view: new View({
                center: this.center,
                zoom: this.zoom
            })
        });
    },
    methods: {
        updateLayer() {
            this.map.getLayers().forEach(function(layer) {
                layer.setSource(null);
            });
            this.map.addLayer(new TileLayer({
                source: new TileWMS({
                    extent: [-13884991, 2870341, -7455066, 6338219],
                    url: this.baseURL,
                    params: {
                        'LAYERS': this.layer,
                        'TILED': true
                    },
                    serverType: this.serverType,
                    crossOrigin: this.crossOrigin,
                    attributions: this.customAttributions
                })
            }));
        }
    }

}
</script>

<style scoped>
.map {
    height: 800px;
    width: 1000px;
}
</style>