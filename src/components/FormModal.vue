<template>
  <div class="layout-padding row justify-center">
    <q-field
      :icon="$props.icon"
      :label="$props.label"
      :helper="$props.helper"
    >
      <q-search
        v-model="model"
        :icon="$props.insetIcon"
        :placeholder="$props.placeholder"
        :debounce="$props.debounce"
        :name="$props.name"
        :autofocus="$props.autofocus"
      >
        <q-autocomplete
          :filter="$props.filter"
          :static-data="$props.staticData"
        />
      </q-search>
    </q-field>

    <q-btn flat round color="primary" @click="openModal">
      <q-icon name="add" />
    </q-btn>

    <q-modal
      ref="modal"
      :maximized="$props.maximized"
      :minimized="$props.minimized"
      :content-css="{ padding: '50px' }"
    >
      <slot></slot>
      <q-btn flat round color="primary" @click="closeModal">
        <q-icon name="close" />
      </q-btn>
    </q-modal>

  </div>
</template>

<script>
import {
  QBtn,
  QIcon,
  QModal,
  QField,
  QSearch,
  QAutocomplete
} from 'quasar'

export default {
  name: 's-form-modal',
  components: {
    QField,
    QIcon,
    QModal,
    QSearch,
    QAutocomplete,
    QBtn
  },
  props: {
    maximized: {
      type: Boolean
    },
    minimized: {
      type: Boolean
    },
    autofocus: {
      type: Boolean
    },
    debounce: {
      type: Number,
      default: 300
    },
    name: {
      type: String
    },
    icon: {
      type: String
    },
    label: {
      type: String
    },
    placeholder: {
      type: String,
      default: ''
    },
    helper: {
      type: String
    },
    staticData: {
      type: Object
    },
    filter: {
      type: Function
    },
    insetIcon: {
      type: String,
      default: ''
    }
  },
  data () {
    return {
      model: ''
    }
  },
  methods: {
    openModal () {
      this.$refs.modal.open()
    },
    closeModal () {
      this.$refs.modal.close()
    },
    search (terms, done) {
      this.$emit('search', terms, done)
    },
    selected (item) {
      this.$emit('selected', item)
    }
  }
}
</script>
