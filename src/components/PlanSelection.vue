//方案选择组件
<template>
  <div>
    <div v-if="coverageList.length < 4">
      <r-tab :tabItems="tabItems" />
      <r-swiper height="600px" :model="index" onChange=this.onIndexChange>
        <r-swiper-item v-for="(item,idx) in items" :key="idx">
          <r-card :title="$t('planSelection.guaranteeRate')">
            <r-table :data="item.planData" :class="{table:classStatus}" />
            <div v-for="(coverage, idx) in coverageList" :key="idx">
              <r-row :model="coverage" value="coverageAmount" class="fa-edit" :onClick="openCoverageDescription.bind(this, coverage)">
                <span class="fa fa-angle-down fa-1x">{{coverage.coverageTitle}}</span>
              </r-row>
              <template v-if="coverage.showDescription">
                <div>
                  <p class="coverageDescription">-在保险期间内，被保险人持有效客票乘坐民航班机，在交通工具内因发生交通事故而遭受意外的，则自遭受该意外之日起一百八十日内以该意外为直接、完全原因而身故或伤残的，保险人按照合同约定给付保险金。</p>
                </div>
              </template>
            </div>
          </r-card>
          <r-card :title="$t('planSelection.notes')">
            <r-list :data="getListData" />
          </r-card>
        </r-swiper-item>
      </r-swiper>
    </div>
    <div v-else>
      <r-card :title="$t('planSelection.guaranteeRate')">
        <r-selector :title="$t('planSelection.plan')" :options="options" :model="selectorModel" value="selectorValue" class="planSelectionSelector"></r-selector>
        <r-table :data="items[0].planData" :class="{table:classStatus}" />
        <div v-for="(coverage, idx) in coverageList" :key="idx">
          <!-- <r-row :value="$t('row.protected')" :model="coverage" :isLink="true">
          <span class="fa fa-lock fa-2x">{{$t('dfdsa')}}</span>
        </r-row> -->
          <r-row :model="coverage" value="coverageAmount" :onClick="openCoverageDescription.bind(this, coverage)">
            <span class="fa fa-angle-down fa-1x">{{coverage.coverageTitle}}</span>
          </r-row>
          <template v-if="coverage.showDescription">
            <div>
              <p class="coverageDescription">-在保险期间内，被保险人持有效客票乘坐民航班机，在交通工具内因发生交通事故而遭受意外的，则自遭受该意外之日起一百八十日内以该意外为直接、完全原因而身故或伤残的，保险人按照合同约定给付保险金。</p>
            </div>
          </template>
        </div>
      </r-card>
      <r-card :title="$t('planSelection.notes')">
        <r-list :data="getListData" />
      </r-card>
    </div>
  </div>
</template>
<script>
import '../i18n/planSelection';
export default {
  data: function() {
    return {
      selectorModel: {
        selectorValue: 0
      },
      items: [
        {
          planData: {
            head: [[{ text: '保险责任' }, { text: '保险金额' }]]
            // body: [
            //   [{ text: "公共交通意外伤害-飞机" }, { text: "50万" }],
            //   [{ text: "公共交通意外伤害-火车(地铁、轻轨)" }, { text: "40万" }],
            //   [{ text: "公共交通意外伤害-汽车" }, { text: "30万" }]
            // ]
          }
        },
        {
          planData: {
            head: [[{ text: '保险责任' }, { text: '保险金额' }]]
            // body: [
            //   [{ text: "公共交通意外伤害-飞机" }, { text: "70万" }],
            //   [{ text: "公共交通意外伤害-火车(地铁、轻轨)" }, { text: "60万" }],
            //   [{ text: "公共交通意外伤害-汽车" }, { text: "50万" }]
            // ]
          }
        },
        {
          planData: {
            head: [[{ text: '保险责任' }, { text: '保险金额' }]]
            // body: [
            //   [{ text: "公共交通意外伤害-飞机" }, { text: "100万" }],
            //   [{ text: "公共交通意外伤害-火车(地铁、轻轨)" }, { text: "90万" }],
            //   [{ text: "公共交通意外伤害-汽车" }, { text: "80万" }]
            // ]
          }
        }
      ],
      coverageItemList: [],
      index: 0,
      classStatus: true,
      coverageList: [
        {
          coverageTitle: '公共交通意外伤害-飞机',
          coverageAmount: '50万',
          coverageDescription:
            '-在保险期间内，被保险人持有效客票乘坐民航班机，在交通工具内因发生交通事故而遭受意外的，则自遭受该意外之日起一百八十日内以该意外为直接、完全原因而身故或伤残的，保险人按照合同约定给付保险金。',
          showDescription: true
        },
        {
          coverageTitle: '公共交通意外伤害-火车(地铁、轻轨)',
          coverageAmount: '70万',
          coverageDescription:
            '-在保险期间内，被保险人持有效客票乘坐民航班机，在交通工具内因发生交通事故而遭受意外的，则自遭受该意外之日起一百八十日内以该意外为直接、完全原因而身故或伤残的，保险人按照合同约定给付保险金。',
          showDescription: true
        },
        {
          coverageTitle: '公共交通意外伤害-汽车',
          coverageAmount: '100万',
          coverageDescription:
            '-在保险期间内，被保险人持有效客票乘坐民航班机，在交通工具内因发生交通事故而遭受意外的，则自遭受该意外之日起一百八十日内以该意外为直接、完全原因而身故或伤残的，保险人按照合同约定给付保险金。',
          showDescription: true
        },
        {
          coverageTitle: '公共交通意外伤害-汽车',
          coverageAmount: '100万',
          coverageDescription:
            '-在保险期间内，被保险人持有效客票乘坐民航班机，在交通工具内因发生交通事故而遭受意外的，则自遭受该意外之日起一百八十日内以该意外为直接、完全原因而身故或伤残的，保险人按照合同约定给付保险金。',
          showDescription: true
        }
      ],
      options: []
    };
  },
  computed: {
    // Tab选项卡的名称
    tabItems: function() {
      return [
        {
          selected: true,
          showdot: false,
          disabled: false,
          bage: '',
          text: '基础版',
          onClick: this.onTabItemClicked
        },
        {
          selected: false,
          showdot: false,
          disabled: false,
          bage: '',
          text: '升级版',
          onClick: this.onTabItemClicked
        },
        {
          selected: false,
          showdot: false,
          disabled: false,
          bage: '',
          text: '尊享版',
          onClick: this.onTabItemClicked
        }
      ];
    },
    getListData() {
      return [
        {
          label: this.$t('planSelection.approvalCrowd'),
          value: '各个年龄段人群'
        },
        { label: this.$t('planSelection.limitPurchase'), value: '10份' },
        { label: this.$t('planSelection.term'), value: '1年' },
        {
          label: this.$t('planSelection.specialInstructions'),
          value: '本产品最终解释权由中国大地保险所有'
        }
      ];
    }
  },
  methods: {
    onIndexChange: function(value) {
    },
    onTabItemClicked: function(index) {
      this.index = index;
    },
    openCoverageDescription(coverage, event) {
      coverage.showDescription = !coverage.showDescription;
    }
  },
  created: function() {
    let count = 0;
    this.coverageList.forEach(element => {
      this.options.push({
        key: count,
        value: element.coverageTitle
      });
      count++;
    });
  },
  mounted: function() {
  }
};
</script>
<style scoped>
.weui-panel__hd {
  text-align: left;
}
.table > table > thead > tr > th:first-child {
  float: left;
  margin-left: 15px;
  color: #999999;
  border: none;
}
.table > table > thead > tr > th:last-child {
  float: right;
  margin-right: 15px;
  color: #999999;
  border: none;
}
.table > table > thead > tr {
  border-bottom: 1px solid #e5e5e5;
}
.coverageDescription {
  margin-left: 20px;
  text-align: left;
  margin-right: 20px;
  font-size: 14px;
}
.swiperHeight {
  min-height: 300px;
}
.planSelectionSelector >div>.weui-cell__ft>span{
  color:green;
}
.fa{
  color: black;
}
</style>
<i18n>

</i18n>