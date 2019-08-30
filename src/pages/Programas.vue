<template>
  <q-page padding>
    <!-- content -->
    <!-- <h1>Programas</h1> -->
    <div class="row q-col-gutter-sm">
      <div class="col-md-3 col-12" v-for="(card,index) in programas" :key="index">
        <q-card flat bordered class="my-card">
          <q-img :src="card.image.medium">
              <div class="absolute-top-right text-subtitle2">
                  {{card.schedule.days[0]}}: {{card.schedule.time}}
                </div>
          </q-img>
          <q-card-section>
            <div class="text-h6">{{card.name}}</div>
            <div class="text-subtitle2">{{card.genres[0]}}, {{card.genres[1]}}, {{card.genres[2]}}</div>
          </q-card-section>
          <q-card-section>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
          </q-card-section>
          <!-- <q-card-section>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
          </q-card-section> -->
          <q-card-actions>
              <q-btn push glossy class="full-width" color="primary">Detalles</q-btn>
              <!-- <q-btn flat>Action 2</q-btn> -->
            </q-card-actions>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'Programas',
  data () {
    return {
      programas: []
    }
  },
  mounted () {
    this.getProgramas()
  },
  methods: {
    getProgramas () {
      this.$q.loading.show({
        spinnerColor: 'blue'
      })
      this.$axios.get('http://api.tvmaze.com/shows?page=0').then((res) => {
        this.programas = res.data
        this.$q.loading.hide({})
        console.log('PROGRAMAS', res)
      }).catch((err) => {
        this.$q.loading.hide({})
        console.error(err)
      })
    }
  }
}
</script>
<style>
</style>
