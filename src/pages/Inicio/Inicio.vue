<template>
    <v-row class="home">
        <v-col cols='12'> 
          <img alt="HubVet logo" src="../../assets/img/logo.png" width="297" height="92"> 
          <Input
            id="text_search"
            name="text_search"
            solo
            label="Copacabana"
            background-color="#FFF"
            autofocus
            class="text-input-home"
            prepend-inner-icon="mdi-magnify"
            v-model="filters.search"
          />
          <div class="content-filter">
              <div class="filters">
                <Autocomplete
                    id="type"
                    name="type"
                    label="Buscar por"
                    placeholder="Pacotes"
                    :items="datasource_type"
                    itemText="nome"
                    itemValue="id"                    
                    v-model="filters.type"
                />
                <Input
                    id="local"
                    name="local"
                    label="Onde você está?"
                    class="ml-43"
                    v-model="filters.local"
                />         
                <ToggleButton
                    id="moeda"
                    name="moeda"
                    label="Milhas ou R$"
                    v-model="filters.moeda">
                    <v-btn value="milha">
                        <img alt="Milhas" src="../../assets/img/milhas.png" width="18" height="13"> 
                    </v-btn>
                    <v-btn value="real">
                        <img alt="Real" src="../../assets/img/money.png" > 
                    </v-btn>
                </ToggleButton>   
                <Autocomplete
                    id="chips_category"
                    name="chips_category"
                    label="Etiquetas"
                    v-model="filters.category"
                    multiple
                    chips
                    small-chips
                    class="ml-43"
                    :items="datasource_category"
                    itemText="nome"
                    itemValue="id"
                    :chipsValue="true"
                >
                </Autocomplete>
               </div>    
                <Button
                    id="btn_search"
                    name="btn_search"
                    class="btn-action"
                    x-large
                    tile
                    color="#44BBA4"
                    dark
                    @click="pesquisar"
                >
                    Pesquisar
                </Button>
          </div>
        </v-col>
    </v-row>
</template>

<script>
import { mapActions, mapGetters } from 'vuex';

export default {
  data() {
    return {
    filters: {
        search: null,
        category: null,
        moeda: 'real',
        local: null,
        type: null,
      },
    };
  },
  computed: {
    ...mapGetters('inicio', {
        datasource_type: 'datasource_type',
        datasource_category: 'datasource_category'
    }),
  },
  methods: {
    ...mapActions('inicio', {
      set_filters: 'set_filters',
      carregar_type: 'carregar_type',
      carregar_category: 'carregar_category'
    }),
    async pesquisar() {
      await this.set_filters({
        filters: this.filters,
      });
      this.$router.push('/viagens')
    }
   },
   async created() {
     await this.carregar_type();
     await this.carregar_category();
   }
};
</script>

<style >
.btn-action {
    padding: 7px 54px!important;
    font-size: 1.27rem;
    margin-top: 63px;
}
</style>

<style scoped>
.home {
    position: absolute;
    top: 50%;
    left: 50%;
    margin-right: -50%;
    transform: translate(-50%, -50%);
}

.text-input-home  {
    width: 416px;
    max-width: 416px;
    border-radius: 8px;
    margin: 28px auto 0px auto;
}

.ml-43 {
    margin-left: 43px;
}

.content-filter {
    min-width: 931px;
}

.filters {
    display: flex;
}

</style>