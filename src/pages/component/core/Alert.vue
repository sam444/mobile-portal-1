<template>
  <r-page>
       <top :title="$t('component.dialog')" :showBack="true"/>
       <r-body>
            <r-card :title="$t('component.basic')">
              <r-switch :title="$t('alert.show')" :model="policy" value="show1" :onClick="onClick"></r-switch>
              <r-switch :title="$t('common.api')" :model="policy" value="show2" :onClick="clickSwitchApi"></r-switch>
              <r-alert  :model="policy" value="show1" :title="$t('alert.title')" :onHide="onHide" :onShow="onShow" > {{ $t('alert.sogo') }}</r-alert>
            </r-card>
       </r-body>
       <bottom :index="2"/>
  </r-page>
</template>

<script>

import '../../../i18n/alert';
import '../../../i18n/component';

export default {
  data() {
    return {
      policy: {}
    };
  },
  methods: {
    onClick() {
      /* eslint-disable */
      console.log('click');
      /* eslint-disable */
    },
    clickSwitchApi(val) {
      const self = this;
      AlertApi.show({
        title: this.$t('alert.title'),
        content: this.$t('alert.sogo'),
        onShow() {
          /* eslint-disable */
          console.log("Module: I'm showing");
          /* eslint-disable */
        },
        onHide() {
          self.policy.show2 = false;
          /* eslint-disable */
          console.log("Module: I'm hiding now");
          /* eslint-disable */
        }
      });
    },
    onHide() {
      /* eslint-disable */
      console.log('Hide');
      /* eslint-disable */
    },
    onShow() {
      /* eslint-disable */
      console.log('show');
      /* eslint-disable */
    }
  }
};
</script>



