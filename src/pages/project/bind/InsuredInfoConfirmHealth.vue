<template>
    <r-page>
        <top :title="$t('project.jtyw')" :showBack="true" />
        <r-body>
            <!-- 保险期限选择 -->
            <r-card>
                <poi type="day" :model="policy.policyData" effectiveDate="effectiveDate" expireDate="expireDate" :readonly="true" />
            </r-card>
            <!-- 投保人信息 -->
            <r-card :title="$t('common.holderInfo')">
                <holder-info :model="policy.holderInfo" :readonly="true" />
            </r-card>
            <!-- 被保人信息 -->
            <r-card :title="$t('common.insuredInfo')">
                <choose-relationship :datas="datas1" :model="policy.insuredInfo" value="relationToHolder" :title="$t('holderInfo.relationToHolder')" :readonly="true" />
                <insured-info v-if="policy.insuredInfo.relationToHolder != '1'" :model="policy.insuredInfo" :readonly="true" />
                <r-row :model="pageModel" :title="$t('insuredInfoEntryHealthSub.healthInfo')" :isLink="true" :onClick="gotoHealthInfo" />
            </r-card>
        </r-body>
        <r-tab-bar>
            <proposal-confirm amount="50" :buttonName="'proposalConfirm.submitPay'" :onClick="goto" />
        </r-tab-bar>
    </r-page>
</template>

<script>
import ChooseRelationship from '../../../components/ChooseRelationship';
import ProposalConfirm from '../../../components/ProposalConfirm';
import HolderInfo from '../../../components/HolderInfo';
import InsuredInfo from '../../../components/InsuredInfo';
import SubsidiaryInsuredInfo from '../../../components/SubsidiaryInsuredInfo';
import ProposalClauseConfirm from '../../../components/ProposalClauseConfirm';
import Poi from '../../../components/Poi';
import '../../../i18n/insuredInfoEntryHealthSub';
import '../../../i18n/proposalConfirm';
import '../../../i18n/holderInfo';
import {SessionContext} from 'rainbow-foundation-cache';

export default {
  components: {
    ChooseRelationship,
    ProposalConfirm,
    HolderInfo,
    InsuredInfo,
    SubsidiaryInsuredInfo,
    ProposalClauseConfirm,
    Poi
  },
  data() {
    return {
      policy: {
        // holderInfo: {},
        // insuredInfo: {
        //   relationToHolder: "1"
        // },
        // subsidiaryInfo: {
        //   relationToHolder: "1"
        // }
      },
      pageModel: {
        clauseConfirmed: false,
        toastShow: false
      },
      datas1: [
        {
          key: '1',
          value: '本人',
          active: true
          // onClick: this.onClickInsured
        },
        {
          key: '2',
          value: '配偶',
          active: false
          // onClick: this.onClickInsured
        },
        {
          key: '3',
          value: '子女',
          active: false
          // onClick: this.onClickInsured
        },
        {
          key: '4',
          value: '父母',
          active: false
          // onClick: this.onClickInsured
        }
      ],
      readonly: false
    };
  },
  methods: {
    goto: function() {
      SessionContext.remove('policy');
      let route = JSON.parse(SessionContext.get('ROUTE_TYPE'));
      if (route && route.route4 && route.route4 != '') {
        this.$router.push({
            path: '/issue/' + route.route4,
            query: this.$route.query
        });
      }
      // Todo:跳转到下一个页面,去支付
    },
    gotoHealthInfo: function() {
      this.$router.push({
        path: '/project/proposal/ah/HealthInform',
        name: 'HealthInform',
        params: {}
      });
    }
  },
  watch: {},
  computed: {},
  created: function() {
    let policyStr = SessionContext.get('policy');
    this.policy = JSON.parse(policyStr);
    // if (this.$route.params.policy) {
    //   this.policy = this.$route.params.policy;
    // }
  }
};
</script>

<style>

</style>
