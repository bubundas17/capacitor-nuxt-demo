<template>
  <v-layout row wrap>
    <v-flex xs12>
      <v-card>
        <v-card-title>test</v-card-title>
        <v-card-text>
          <v-btn @click="shownotification">Notification</v-btn>
        </v-card-text>
      </v-card>
    </v-flex>

  </v-layout>
</template>

<script>
  import { Plugins } from '@capacitor/core';
  const { LocalNotifications } = Plugins;

export default {
  methods: {
    async shownotification(){
      try {
        await LocalNotifications.schedule({
          notifications: [
            {
              title: "Title",
              body: "Body",
              id: 1,
              schedule: { at: new Date(Date.now() + 1000 * 5) },
              sound: null,
              attachments: null,
              actionTypeId: "",
              extra: null
            }
          ]
        });
      } catch (e) {
        Plugins.Modals.alert({
          title: 'Test Alert',
          message: e
        })
      }
    }

  }

}
</script>
