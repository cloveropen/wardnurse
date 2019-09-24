<template>
  <v-app id="warddoc.cloveropen.com">
    <Basepage />    
    <v-container fluid fill-height>
      <v-layout justify-start>
        <patient />
      </v-layout>
    </v-container>
  </v-app>
</template>

<script>
import Basepage from "../components/Basepage";
import patient from "../components/patientc";
export default {
  components: {
    Basepage,
    patient
  }
};
</script>
