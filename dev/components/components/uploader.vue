<template>
  <div>
    <div class="layout-padding">
      <q-input v-model="url" />
      <br>
      <div class="bg-black q-pa-sm" style="max-width: 500px">
        <q-uploader dark :url="url" multiple color="lime" float-label="Float label" />
        <br>
        <q-uploader dark hide-underline :url="url" multiple color="orange" float-label="Float label" />
        <br>
        <q-field
          icon="wifi"
          label="Wifi network"
          :count="10"
          helper="We need this for connecting you"
        >
          <q-uploader dark :url="url" multiple color="orange" float-label="Float label" />
        </q-field>
        <br>
        <q-field
          icon="wifi"
          label="Wifi network"
          :count="10"
          helper="We need this for connecting you"
        >
          <q-uploader dark inverted :url="url" multiple color="orange" float-label="Float label" />
        </q-field>
      </div>

      <p class="caption">Single File Upload</p>
      <q-uploader style="max-width: 320px" color="amber" stack-label="Stack Label" :url="url" />

      <p class="caption">No Thumbnails</p>
      <q-uploader style="max-width: 320px" no-thumbnails color="amber" :url="url" />

      <q-toggle v-model="inverted" label="Inverted" />
      <q-toggle v-model="dark" label="Dark" />
      <p class="caption">Multiple File Upload</p>
      <div class="q-pa-sm" :class="this.dark ? 'bg-grey-10 text-orange' : ''">
        <q-uploader
          :inverted="inverted"
          :dark="dark"
          auto-expand
          style="max-width: 320px"
          float-label="Upload files"
          multiple
          :url="url"
          ref="upld"
          @start="emit('start')"
          @finish="emit('finish')"
          @uploaded="uploaded"
          @add="add"
          @remove:done="removeDone"
          @remove:abort="removeAbort"
          @remove:cancel="removeCancel"
        />
      </div>

      <q-btn color="primary" @click="pick" style="margin-top: 15px">Pick Files</q-btn>
      <q-btn color="primary" @click="reset" style="margin-top: 15px">Reset the above Uploader</q-btn>

      <p class="caption">Single File Upload - No Upload Button</p>
      <q-uploader style="max-width: 320px" hide-upload-button color="amber" stack-label="Stack Label" :url="url" />

      <p class="caption">No Thumbnails - No Upload Button</p>
      <q-uploader style="max-width: 320px" hide-upload-button no-thumbnails color="amber" :url="url" />

      <p class="caption">Multiple File Upload - No Upload Button</p>
      <q-uploader
        style="max-width: 320px"
        float-label="Upload files"
        multiple
        hide-upload-button
        :url="url"
        @start="emit('start')"
        @finish="emit('finish')"
        @uploaded="uploaded"
        @add="add"
        @remove:done="removeDone"
        @remove:abort="removeAbort"
        @remove:cancel="removeCancel"
      />

      <p class="caption">Single File Upload - No Upload Button - No Upload Progress</p>
      <q-uploader style="max-width: 320px" hide-upload-button hide-upload-progress color="amber" stack-label="Stack Label" :url="url" />

      <p class="caption">No Thumbnails - No Upload Button - No Upload Progress</p>
      <q-uploader style="max-width: 320px" hide-upload-button hide-upload-progress no-thumbnails color="amber" :url="url" />

      <p class="caption">Multiple File Upload - No Upload Button - No Upload Progress</p>
      <q-uploader
        style="max-width: 320px"
        float-label="Upload files"
        multiple
        hide-upload-button
        hide-upload-progress
        :url="url"
        @start="emit('start')"
        @finish="emit('finish')"
        @uploaded="uploaded"
        @add="add"
        @remove:done="removeDone"
        @remove:abort="removeAbort"
        @remove:cancel="removeCancel"
      />

      <div class="absolute-right no-pointer-events">
        <q-btn @click="clear" style="pointer-events: all" color="primary">Clear Debug Log</q-btn>
        <div v-for="evt in events" :key="evt">
          {{evt}}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      url: 'http://1.1.1.195/upload.php',
      events: [],
      inverted: false,
      dark: false
    }
  },
  methods: {
    pick () {
      this.$refs.upld.pick()
    },
    clear () {
      this.events = []
    },
    emit (evt) {
      this.events.push(evt)
    },
    uploaded (file) {
      this.events.push(`uploaded ${file.name}`)
    },
    add (files) {
      this.events.push(`add ${files.length}`)
    },
    removeCancel (file) {
      this.events.push(`remove:cancel ${file.name}`)
    },
    removeAbort (file) {
      this.events.push(`remove:abort ${file.name}`)
    },
    removeDone (file) {
      this.events.push(`remove:done ${file.name}`)
    },

    reset () {
      this.$refs.upld.reset()
    }
  }
}
</script>
