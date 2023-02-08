<template>
  <v-container class="fill-height">
    <v-responsive class="d-flex align-center text-center fill-height">
      <v-img contain height="240" src="@/assets/logo.png" />

      <v-card>
        <v-card-title class="headline">Projeto fullstack </v-card-title>
        <v-card-text>
          <p>
            Um projeto desenvolvido para você conseguir fixar conhecimentos sobre tecnologia
          </p>
          <h3 class="pt-6">Links úteis:</h3>
          <v-btn
            href="https://github.com/huogerac/djavue/"
            min-width="164"
            rel="noopener noreferrer"
            target="_blank"
            variant="text">
            <v-icon icon="mdi-arrow-top-right-bold-box-outline" size="large" start />
            Código deste template
          </v-btn>
          <v-btn
            href="https://next.vuetifyjs.com/en/introduction/why-vuetify/#feature-guides/"
            min-width="164"
            rel="noopener noreferrer"
            target="_blank"
            variant="text">
            <v-icon icon="mdi-semantic-web" size="large" start />
            Vuetify
          </v-btn>
          <v-btn
            href="https://next.vuetifyjs.com/components/all/"
            min-width="164"
            rel="noopener noreferrer"
            target="_blank"
            variant="text">
            <v-icon icon="mdi-view-dashboard" size="large" start />
            Components
          </v-btn>

          <v-btn
            href="https://community.vuetifyjs.com/"
            min-width="164"
            rel="noopener noreferrer"
            target="_blank"
            variant="text">
            <v-icon icon="mdi-account-group" size="large" start />
            Community
          </v-btn>
          <p class="pt-6">
            Achou um problema? Cadastre uma
            <a
              href="https://github.com/huogerac/djavue/issues"
              target="_blank"
              rel="noopener noreferrer"
              title="contribute">
              Issue aqui </a
            >.
          </p>
          <p>Obrigado por utilizar este template.</p>
          <div class="text-xs-right">
            <em><small>&mdash; Tábata de faria 🦋 </small></em>
          </div>
          <hr class="my-3" />
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn color="primary" :to="{ name: 'base-home' }"> Início </v-btn>
        </v-card-actions>
      </v-card>
    </v-responsive>
  </v-container>
</template>

<script setup></script>
