<template>
  <div class="content">
    <a href="#" @click="print">Сохранить</a>
    <div id="map" ref="shareMe">
      <yandex-map
        :coords="[53.9000000, 27.5666700]"
        zoom="11"
        style="width: 600px; height: 600px;"
        :cluster-options="{
    1: {clusterDisableClickZoom: true}
  }"
        map-type="hybrid"
        :scroll-zoom="false"
      >
        <ymap-marker
          v-if="showBlueLine"
          key="line001"
          marker-id="line001"
          marker-type="polyline"
          :coords="blueLine"
          hint-content="Синяя ветка Минского метро"
          :marker-fill="styleBlueFill"
          :marker-stroke="styleBlueStroke"
          :balloon="{header: 'Синяя ветка', body: 'Минское метро', footer: '16 станций, 1 проектируется'}"
        ></ymap-marker>

        <div clas="station" v-if="showBlueLine">
          <ymap-marker
            v-for="station in getStationsBlue"
            :key="station.id"
            :marker-id="station.id"
            marker-type="circle"
            :coords="station.coords"
            circle-radius="200"
            :hint-content="station.name"
            :marker-fill="styleBlueStroke"
            :marker-stroke="styleBlueFill"
            :balloon="{
            header: station.name, 
            body: 'Станция Минского метрополитена. Расположена на Московской линии, между станциями «Октябрьская» и «Институт Культуры». «Площадь Ленина» была открыта 30 июня 1984 года в составе первой очереди минского метро. Является одной из самых загруженных станций метро в Минске — в среднем ей пользуется до 95,2 тыс. человек в сутки', 
            footer: 'Дата открытия: 30 июня 1984 года'
          }"
          ></ymap-marker>
        </div>

        <div clas="station" v-if="showRedLine">
          <ymap-marker
            v-for="station in getStationsRed"
            :key="station.id"
            :marker-id="station.id"
            marker-type="circle"
            :coords="station.coords"
            circle-radius="200"
            :hint-content="station.name"
            :marker-fill="styleRedStroke"
            :marker-stroke="styleRedFill"
            :balloon="{header: 'header', body: 'body', footer: 'footer'}"
          ></ymap-marker>
        </div>

        <div clas="station" v-if="showGreenLine">
          <ymap-marker
            v-for="station in getStationsGreen"
            :key="station.id"
            :marker-id="station.id"
            marker-type="circle"
            :coords="station.coords"
            circle-radius="200"
            :hint-content="station.name"
            :marker-fill="styleGreenStroke"
            :marker-stroke="styleGreenFill"
            :balloon="{header: 'header', body: 'body', footer: 'footer'}"
          ></ymap-marker>
        </div>

        <div clas="station" v-if="showBlueLine">
          <ymap-marker
            v-for="station in getStationsBlueInactive"
            :key="station.id"
            :marker-id="station.id"
            marker-type="circle"
            :coords="station.coords"
            circle-radius="200"
            :hint-content="station.name"
            :marker-fill="styleBlueFill"
            :marker-stroke="styleBlueStroke"
            :balloon="{header: 'header', body: 'body', footer: 'footer'}"
          ></ymap-marker>
        </div>

        <div clas="station" v-if="showRedLine">
          <ymap-marker
            v-for="station in getStationsRedInactive"
            :key="station.id"
            :marker-id="station.id"
            marker-type="circle"
            :coords="station.coords"
            circle-radius="200"
            :hint-content="station.name"
            :marker-fill="styleRedFill"
            :marker-stroke="styleRedStroke"
            :balloon="{header: 'header', body: 'body', footer: 'footer'}"
          ></ymap-marker>
        </div>

        <div clas="station" v-if="showGreenLine">
          <ymap-marker
            v-for="station in getStationsGreenInactive"
            :key="station.id"
            :marker-id="station.id"
            marker-type="circle"
            :coords="station.coords"
            circle-radius="200"
            :hint-content="station.name"
            :marker-fill="styleGreenFill"
            :marker-stroke="styleGreenStroke"
            :balloon="{header: 'header', body: 'body', footer: 'footer'}"
          ></ymap-marker>
        </div>
      </yandex-map>
    </div>
    <!-- OUTPUT -->
    <div class="screenshot">
      <img :src="sharingImage">
    </div>
  </div>
</template>

<script>
import { yandexMap, ymapMarker } from "vue-yandex-maps";
import domtoimage from "dom-to-image";
export default {
  name: "YandexMap",
  props: {
    msg: String
  },
  components: { yandexMap, ymapMarker },
  data() {
    return {
      sharingImage: null,
      showBlueLine: true,
      showRedLine: true,
      showGreenLine: true,
      styleGreenStroke: { color: "#406106", opacity: 0.8, width: 2 },
      styleBlueStroke: { color: "#2e3094", opacity: 0.8, width: 2 },
      styleRedStroke: { color: "#f11a21", opacity: 0.8, width: 2 },
      styleBlueFill: { color: "#fff", opacity: 0.8 },
      styleGreenFill: { color: "#fff", opacity: 0.8 },
      styleRedFill: { color: "#fff", opacity: 0.8 },
      blueLine: [
        [53.848379, 27.474202],
        [53.864788, 27.485843],
        [53.876945, 27.497036],
        [53.886562, 27.514768],
        [53.886053, 27.540352],
        [53.893524, 27.548114],
        [53.902263, 27.56193],
        [53.90927, 27.57527],
        [53.915926, 27.583759],
        [53.922401, 27.600198],
        [53.924288, 27.613143],
        [53.928084, 27.627462],
        [53.934605, 27.651097],
        [53.945565, 27.687676]
      ],
      stations: [
        {
          line: 1,
          name: "Смоленская",
          id: 125,
          coords: [53.951108, 27.706165],
          active: false
        },
        {
          line: 1,
          name: "Малиновка",
          id: 110,
          coords: [53.848379, 27.474202],
          active: true
        },
        {
          line: 1,
          name: "Петровщина",
          id: 111,
          coords: [53.864788, 27.485843],
          active: true
        },
        {
          line: 1,
          name: "Михалово",
          id: 112,
          coords: [53.876945, 27.497036],
          active: true
        },
        {
          line: 1,
          name: "Грушевка",
          id: 113,
          coords: [53.886562, 27.514768],
          active: true
        },
        {
          line: 1,
          name: "Институт Культуры",
          id: 114,
          coords: [53.886053, 27.540352],
          active: true
        },
        {
          line: 1,
          name: "пл. Ленина",
          id: 115,
          coords: [53.893524, 27.548114],
          active: true
        },
        {
          line: 1,
          name: "Октябрьская",
          id: 116,
          coords: [53.902263, 27.56193],
          active: true
        },
        {
          line: 1,
          name: "пл. Победы",
          id: 117,
          coords: [53.90927, 27.57527],
          active: true
        },
        {
          line: 1,
          name: "пл. Я. Коласа",
          id: 118,
          coords: [53.915926, 27.583759],
          active: true
        },
        {
          line: 1,
          name: "Академия Наук",
          id: 119,
          coords: [53.922401, 27.600198],
          active: true
        },
        {
          line: 1,
          name: "Парк Челюскинцев",
          id: 120,
          coords: [53.924288, 27.613143],
          active: true
        },
        {
          line: 1,
          name: "Московская",
          id: 121,
          coords: [53.928084, 27.627462],
          active: true
        },
        {
          line: 1,
          name: "Восток",
          id: 122,
          coords: [53.934605, 27.651097],
          active: true
        },
        {
          line: 1,
          name: "Борисовский тракт",
          id: 123,
          coords: [53.93885, 27.666206],
          active: true
        },
        {
          line: 1,
          name: "Уручье",
          id: 124,
          coords: [53.945565, 27.687676],
          active: true
        },
        {
          line: 2,
          name: "Шабаны",
          id: 209,
          coords: [53.846431, 27.708997],
          active: false
        },
        {
          line: 2,
          name: "Красный Бор",
          id: 224,
          coords: [53.90937, 27.416271],
          active: false
        },
        {
          line: 2,
          name: "Могилевская",
          id: 210,
          coords: [53.861798, 27.673986],
          active: true
        },
        {
          line: 2,
          name: "Автозаводская",
          id: 211,
          coords: [53.868918, 27.648105],
          active: true
        },
        {
          line: 2,
          name: "Партизанская",
          id: 212,
          coords: [53.875353, 27.629627],
          active: true
        },
        {
          line: 2,
          name: "Тракторный завод",
          id: 213,
          coords: [53.890123, 27.614347],
          active: true
        },
        {
          line: 2,
          name: "Пролетарская",
          id: 214,
          coords: [53.890372, 27.586841],
          active: true
        },
        {
          line: 2,
          name: "Первомайская",
          id: 215,
          coords: [53.89379, 27.570949],
          active: true
        },
        {
          line: 2,
          name: "Купаловская",
          id: 216,
          coords: [53.900798, 27.561714],
          active: true
        },
        {
          line: 2,
          name: "Немига",
          id: 217,
          coords: [53.905732, 27.554016],
          active: true
        },
        {
          line: 2,
          name: "Фрунзенская",
          id: 218,
          coords: [53.905408, 27.539319],
          active: true
        },
        {
          line: 2,
          name: "Молодежная",
          id: 219,
          coords: [53.906527, 27.523617],
          active: true
        },
        {
          line: 2,
          name: "Пушкинская",
          id: 220,
          coords: [53.909429, 27.497251],
          active: true
        },
        {
          line: 2,
          name: "Спортивная",
          id: 221,
          coords: [53.908315, 27.480758],
          active: true
        },
        {
          line: 2,
          name: "Кунцевщина",
          id: 222,
          coords: [53.906007, 27.45423],
          active: true
        },
        {
          line: 2,
          name: "Каменная Горка",
          id: 223,
          coords: [53.906602, 27.437415],
          active: true
        },
        {
          line: 3,
          name: "Слуцкий гостинец",
          id: 310,
          coords: [53.84226, 27.533712],
          active: false
        },
        {
          line: 3,
          name: "Неморшанский сад",
          id: 311,
          coords: [53.850077, 27.537596],
          active: false
        },
        {
          line: 3,
          name: "Аэродромная",
          id: 312,
          coords: [53.867383, 27.54679],
          active: false
        },
        {
          line: 3,
          name: "Ковальская Слобода",
          id: 313,
          coords: [53.87803, 27.54978],
          active: true
        },
        {
          line: 3,
          name: "Вокзальная",
          id: 314,
          coords: [53.8895, 27.548013],
          active: true
        },
        {
          line: 3,
          name: "пл. Ф. Багущевича",
          id: 315,
          coords: [53.896512, 27.538089],
          active: true
        },
        {
          line: 3,
          name: "Юбилейная пл.",
          id: 316,
          coords: [53.904268, 27.539945],
          active: true
        }
      ]
    };
  },
  computed: {
    getStationsRed: function() {
      return this.stations.map(el => (el.line === 2 && el.active ? el : ""));
    },

    getStationsRedInactive: function() {
      return this.stations.map(el => (el.line === 2 && !el.active ? el : ""));
    },

    getStationsBlue: function() {
      return this.stations.map(el => (el.line === 1 && el.active ? el : ""));
    },

    getStationsBlueInactive: function() {
      return this.stations.map(el => (el.line === 1 && !el.active ? el : ""));
    },

    getStationsGreen: function() {
      return this.stations.map(el => (el.line === 3 && el.active ? el : ""));
    },

    getStationsGreenInactive: function() {
      return this.stations.map(el => (el.line === 3 && !el.active ? el : ""));
    }
  },
  methods: {
    /*async print() {
      const el = this.$refs.shareMe;
      // add option type to get the image version
      // if not provided the promise will return
      // the canvas.
      const options = {
        type: "dataURL"
      };
      this.sharingImage = await this.$html2canvas(el, options);
    }*/
    print() {
      var node = document.getElementById('map');

      domtoimage.toPixelData(node)
          .then(function (pixels) {
              for (var y = 0; y < node.scrollHeight; ++y) {
                for (var x = 0; x < node.scrollWidth; ++x) {
                  let pixelAtXYOffset = (4 * y * node.scrollHeight) + (4 * x);
                  /* pixelAtXY is a Uint8Array[4] containing RGBA values of the pixel at (x, y) in the range 0..255 */
                  let pixelAtXY = pixels.slice(pixelAtXYOffset, pixelAtXYOffset + 4);
                }
              }
          });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.screenshot {
  border: 1px solid red;
  width: 600px;
  height: 600px;
}
</style>
