<template>
    <v-autocomplete
      :id="id"
      :name='name'
      :label="label"
      :prepend-inner-icon="prependInnerIcon"
      :solo='solo'
      :autofocus="autofocus"
      hide-no-data
      hide-selected
      :placeholder="placeholder"
      :chips="chips"
      :small-chips="smallChips"
      :multiple="multiple"
    ></v-autocomplete>
</template>

<script>

export default {
  name: 'Autocomplete',
  props: {
    // PROPRIEDADES DE LAYOUT
    /**
     * Identificador único para todo o documento.
     */
    id: {
      type: String,
      required: true,
    },
    /**
     * Identificação do elemento no formulário.
     */
    name: {
      type: String,
      required: true,
    },   
    /**
     * Etiqueta de entrada (texto antes da entrada)
     */
    label: {
      type: String,
      required: false,
    },
    /**
     * Dica que descreve o valor esperado de um campo de entrada
     */
    placeholder: {
      type: String,
      required: false,
    },
    /**
     * Habilita o foco em um elemento.
     */
    autofocus: {
      type: Boolean,
      default: false,
      required: false,
    },
    /**
     * Habilita o Solo em um elemento.
     */
    solo: {
      type: Boolean,
      default: false,
      required: false,
    },
    /**
     * Habilita o Chips em um elemento.
     */
    chips: {
      type: Boolean,
      default: false,
      required: false,
    },
    /**
     * Habilita o Multiple em um elemento.
     */
    multiple: {
      type: Boolean,
      default: false,
      required: false,
    },
    /**
     * Habilita o small-chips em um elemento.
     */
    smallChips: {
      type: Boolean,
      default: false,
      required: false,
    },
    /**
     * Cor Background customizado para elemento.
     */
    backgroundColor: {
      type: String,
      required: false,
    },  
    /**
     * Icon Prepend Inner Icon.
     */
    prependInnerIcon: {
      type: String,
      required: false,
    },    
    // PROPRIEDADES DE DADOS
    /**
     * Valor de ligação (value / v-model)
     */
    value: {
      default: '',
      require: false,
    },
  },
  data() {
    return {
      model: '',
    };
  },
  methods: {
    clear() {
      this.$emit('clear', this.id);
    },
  },
  watch: {
    value(value) {
      this.model = value;
    },
    model(value) {
      this.$emit('input', value);
    },
  },
};
</script>