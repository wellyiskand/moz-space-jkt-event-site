<template>
  <form class="pa-4">
    <h3>Infomasi komunitas / organisasi</h3>
    <v-text-field
      v-model="name"
      label="Nama Komunitas / Organisasi"
      :error-messages="errors.collect('name')"
      v-validate="'required'"
      data-vv-name="name"
      required
    ></v-text-field>
    <v-text-field
      v-model="pic"
      label="Atas Nama Penanggung Jawab"
      :error-messages="errors.collect('pic')"
      v-validate="'required'"
      data-vv-name="pic"
      required
    ></v-text-field>
    <v-text-field
      v-model="description"
      label="Deskripsi singkat tentang komunitas kamu"
      :error-messages="errors.collect('description')"
      v-validate="'required'"
      data-vv-name="description"
      required
    ></v-text-field>
    <v-text-field
      v-model="email"
      label="E-mail"
      :error-messages="errors.collect('email')"
      v-validate="'required|email'"
      data-vv-name="email"
      required
    ></v-text-field>
    <v-text-field
      v-model="phone"
      label="Nomor Telfon / Whatsapp"
      :error-messages="errors.collect('phone')"
      v-validate="'required'"
      data-vv-name="phone"
      required
    ></v-text-field>
    <v-text-field
      v-model="website"
      label="Website"
      :error-messages="errors.collect('website')"
      v-validate="''"
      data-vv-name="website"
    ></v-text-field>
    <v-text-field
      v-model="instagramLink"
      label="Tautan Instagram, contoh : instagram.com/mozillaindonesia/"
      :error-messages="errors.collect('instagramLink')"
      v-validate="''"
      data-vv-name="instagramLink"
    ></v-text-field>
    <v-text-field
      v-model="twitterLink"
      label="Tautan Twitter, Contoh: twitter.com/ID_Mozilla "
      :error-messages="errors.collect('twitterLink')"
      v-validate="''"
      data-vv-name="twitterLink"
    ></v-text-field>
    <v-text-field
      v-model="facebookLink"
      label="Tautan Facebook"
      :error-messages="errors.collect('facebookLink')"
      v-validate="''"
      data-vv-name="facebookLink"
    ></v-text-field>
  </form>
</template>
<script>
export default {
  $_veeValidate: {
    validator: 'new'
  },
  data () {
    return {
      pic: '',
      name: '',
      email: '',
      phone: '',
      website: '',
      instagramLink: '',
      twitterLink: '',
      facebookLink: '',
      description: '',
      organization: '', // will be called from parent component
    }
  },
  methods: {
    submit() {
      this.$validator.validateAll().then(isFormValid => {
        if (isFormValid) {
          this.$emit('startLoading')
          this.$axios.$post(`/Organizations`, {
            name: this.name,
            pic: this.pic,
            email: this.email,
            phone: this.phone,
            description: this.description,
            website: this.website,
            instagramLink: this.instagramLink,
            twitterLink: this.twitterLink,
            facebookLink: this.facebookLink
          }).then(res => {
            this.organization = res;
            this.$emit('organizationFormSubmitted')
          }).catch(err => {
            this.$store.dispatch('notify', { type: 'error', message: err.message })
          })
        }
      })
    }
  }
}
</script>
