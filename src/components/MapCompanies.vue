<template>
  <section class="map-container" :class="{'is-loading': !companies.length }">
    <div>
      <ol-map
        :loadTilesWhileAnimating="true"
        :loadTilesWhileInteracting="true"
        class="map"
      >
        <ol-view
          ref="view"
          :center="center"
          :rotation="rotation"
          :zoom="zoom"
          :projection="projection"
        />

        <ol-tile-layer>
          <ol-source-osm />
        </ol-tile-layer>

        <ol-vector-layer>
          <ol-source-vector ref="vectorsource">
          <ol-animation-fade :duration="4000">
            <ol-feature v-for="index in 2" :key="index">
              <ol-geom-multi-point
                :coordinates="coordinates"
              ></ol-geom-multi-point>

              <ol-style>
                <ol-style-icon :src="markerIcon" :scale="0.3"></ol-style-icon>
              </ol-style>
            </ol-feature>
          </ol-animation-fade>
        </ol-source-vector>
        </ol-vector-layer>
      </ol-map>

      <q-card class="card-company">
        <q-card-section class="q-pa-none card-company__header">
          <div class="text-h5">Nome da Empresa</div>
          <div>Nome do representante</div>
          <q-item-section class="icon" avatar>
              <q-icon name="domain" />
          </q-item-section>
        </q-card-section>

        <q-card-section class="card-company__body q-pa-none">
          <div class="row item">
            <div class="col-12 col-sm-5">
              <q-item-section class="icon" avatar>
                <q-icon name="mail" />
              </q-item-section>
              <span>E-mail</span>
            </div>
            <div class="col-12 col-sm-7">
              <span class="text">email@email.com</span>
            </div>
          </div>
          <div class="row item">
            <div class="col-12 col-sm-5">
              <q-item-section class="icon" avatar>
                <q-icon name="location_on" />
              </q-item-section>
              <span>Localização</span>
            </div>
            <div class="col-md-7">
              <span class="text">Cidade - UF</span>
            </div>
          </div>
          <div class="row item">
            <div class="col-12 col-sm-5">
              <q-item-section class="icon" avatar>
                <q-icon name="category" />
              </q-item-section>
              <span>Categoria</span>
            </div>
            <div class="col-12 col-sm-7">
              <span class="text solid">Categoria</span>
            </div>
          </div>
        </q-card-section>
      </q-card>
    </div>
  </section>
</template>

<script>
  import { defineComponent, ref, inject, onMounted } from 'vue'

  import markerIcon from "../assets/marker.svg";
import { api } from 'src/boot/axios';

  export default defineComponent({
    name: 'MapCompanies',

    setup () {
      const center = ref([-53.3983, -11.5298]);
      const projection = ref('EPSG:4326');
      const zoom = ref(5);
      const rotation = ref(0);

      const format = inject('ol-format');
      const geoJson = new format.GeoJSON();

      const companies = ref([])
      const coordinates = ref([])

      const loadCompanies = async () => {
        const response = await api.get(`/api/companies`)
        companies.value = response.data.data

        coordinates.value = response.data.data.map((coordinate) => {
          return [coordinate.longitude, coordinate.latitude]
        })
      }

    onMounted(() => {
      loadCompanies()
    })

      return {
        center,
        projection,
        zoom,
        rotation,
        geoJson,
        markerIcon,
        coordinates,
        companies,
        loadCompanies
      }
    }
  });
</script>

<style lang="scss">
  @keyframes lds-dual-ring {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }

  .map-container {
    width: 100%;
    height: calc(100vh - 120px);
    border-radius: 18px;
    margin-top: 16px;
    background-color: #dfdfdf;
    overflow: hidden;
    position: relative;

    &.is-loading {
      pointer-events: none;

      > div {
        height: inherit;
        filter: blur(4px);
      }

      &:after {
        content: '';
        position: absolute;
        z-index: 2;
        top: calc(50% - 25px);
        left: calc(50% - 25px);
        display: block;
        width: 60px;
        height: 60px;
        border-radius: 50%;
        border: 7px solid $labels;
        border-color: $labels $labels $labels transparent;
        animation: lds-dual-ring 1.2s linear infinite;
      }
    }

    .map {
      position: absolute;
      inset: 0;
    }

    .map-icon {
      width: 30px;
      height: 30px;
    }

    .card-company {
      position: absolute;
      left: 20px;
      bottom: 20px;
      width: 420px;
      max-width: calc(100% - 40px);
      border-radius: 16px;
      color: $labels;
      padding: 25px 20px 30px;

      .icon {
        min-width: auto;
        padding-right: 10px;
      }

      &__header {
        padding-right: 55px;
        border-radius: 0;
        position: relative;

        .text-h5 {
          line-height: 1.1;
        }

        .icon {
          position: absolute;
          right: 0;
          top: 1px;
        }
      }

      &__body {
        .item {
          margin-top: 12px;
          > div {
            &:first-child {
              display: flex;
              color: #aaa;
              align-items: center;

              .icon {
                transform: translateY(-1px);

                i {
                  font-size: 20px;
                }
              }
            }
          }

          .text {
            display: inline-block;

            @media (max-width: $breakpoint-xs-max) {
              margin-top: 5px;
            }
          }

          .solid {
            padding: 6px 15px;
            border-radius: 50px;
            margin-top: -6px;
            background-color: $background-light;

            @media (max-width: $breakpoint-xs-max) {
              margin-top: 5px;
            }
          }
        }
      }
    }
  }
</style>
