<template>
  <r-page>
    <top :title="$t('common.autoPassengersInsurance')" :showBack="true" />
    <r-body>
      <r-card :title="$t('planSelection.term')">
        <poi type="day" :model="policy.policyData" expireDate="expireDate" effectiveDate="effectiveDate" />
      </r-card>
      <r-card :title="$t('common.holder')">
        <holder-info v-bind:readonly="readonly" v-bind:model="policy.holderInfo"></holder-info>
      </r-card>
      <r-card :title="$t('insuredInfoEntryPassenger.carInfo')">
        <r-input :title="$t('insuredInfoEntryPassenger.model')" :required="true" :model="policy.carInfo" value="carModel" :onChange="getCarModel" :readonly="readonly" />
        <r-input :title="$t('insuredInfoEntryPassenger.licenseNo')" :required="true" :model="policy.carInfo" value="licenseNo" :onChangle="getCarModel" :readonly="readonly" />
        <r-input :title="$t('insuredInfoEntryPassenger.engineNo')" :required="true" :model="policy.carInfo" value="engineNo" :onChange="getCarModel" :readonly="readonly" />
        <r-input :title="$t('insuredInfoEntryPassenger.vin')" :required="true" :model="policy.carInfo" value="vin" :onChange="getCarModel" :readonly="readonly" />
        <r-input :title="$t('insuredInfoEntryPassenger.approvalSeatNum')" :required="true" :model="policy.carInfo" value="approvalSeatCount" :onChange="getCarModel" :readonly="readonly" />
        <r-input :title="$t('insuredInfoEntryPassenger.carOwner')" :required="true" :model="policy.carInfo" value="drivingLicenseOwner" :onChange="getCarModel" :readonly="readonly" />
        <r-selector :title="$t('insuredInfoEntryPassenger.carUsage')" :options="options" :model="policy.carInfo" value="vehicleUseNatureCode" :onChange="getVehicleUseNatureCode" :readonly="readonly"></r-selector>
      </r-card>
      <proposal-clause-confirm :model="pageModel" value="clauseConfirm" />
      <!-- 未确认条款后弹出的提示框 -->
      <r-toast :model="pageModel" value="toastShow" :text="$t('insuredInfoEntryHealthSub.toast')" type="text" />
    </r-body>
    <r-tab-bar>
      <proposal-confirm :buttonName="buttonName" :amount="amount" :onClick="onClick"></proposal-confirm>
    </r-tab-bar>
  </r-page>
</template>

<script>
import Poi from '../../../components/Poi';
import HolderInfo from '../../../components/HolderInfo';
import ProposalConfirm from '../../../components/ProposalConfirm';
import ProposalClauseConfirm from '../../../components/ProposalClauseConfirm';
import '../../../i18n/insuredInfoEntryPassenger';
import '../../../i18n/planSelection';
import '../../../i18n/insuredInfoEntryHealthSub';
import {SessionContext} from 'rainbow-foundation-cache';
export default {
  components: {
    Poi,
    HolderInfo,
    ProposalConfirm,
    ProposalClauseConfirm
  },
  props: {},
  data() {
    return {
      readonly: true,
      policy: {
        // effectiveDate: "",
        // expireDate: "",
        // holderInfo: {},
        // carInfo: {}
      },
      options: [{ key: '1', value: '家庭自用' }],
      buttonName: 'proposalConfirm.submitPay',
      amount: '100',
      pageModel: {
        clauseConfirm: false,
        toastShow: false
      }
    };
  },
  created: function() {
    this.policy = JSON.parse(SessionContext.get('policy'));
  },
  mounted: function() {},
  methods: {
    getCarModel: function() {
    },
    getVehicleUseNatureCode: function() {
    },
    onClick: function() {
      if (this.pageModel.clauseConfirm) {
        SessionContext.remove('policy');
        let route = JSON.parse(SessionContext.get('ROUTE_TYPE'));
        if (route && route.route4 && route.route4 != '') {
          this.$router.push({
            path: '/issue/' + route.route4,
            query: this.$route.query,
            params: [
              {
                name: 'test',
                dataObj: this.policy
              },
              {
                name: 'test2',
                dataObj: this.policy
              }
            ]
          });
        }
        // this.$router.push({
        //   path: "/project/proposal/payStatus",
        //   name: "PayStatus",
        //   params: [
        //     {
        //       name: "test",
        //       dataObj: this.policy
        //     },
        //     {
        //       name: "test2",
        //       dataObj: this.policy
        //     }
        //   ]
        // });
      } else {
        this.pageModel.toastShow = true;
      }
    }
  },
  watch: {
    'pageModel.clauseConfirm': {
      handler: function() {
      }
    }
  }
};
</script>

<style>

</style>
