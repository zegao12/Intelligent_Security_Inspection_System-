<template>
  <div>
    <a-row :gutter="24">
      <a-col :sm="24" :md="12" :xl="6" :style="{ marginBottom: '24px' }">
        <chart-card :loading="loading" :title="$t('dashboard.analysis.total-sales')" total="126,560件">
          <a-tooltip :title="$t('dashboard.analysis.introduce')" slot="action">
            <a-icon type="info-circle-o" />
          </a-tooltip>
          <div>
            <trend flag="up" style="margin-right: 16px;">
              <span slot="term">{{ $t('dashboard.analysis.week') }}</span>
              12%
            </trend>
            <trend flag="down">
              <span slot="term">{{ $t('dashboard.analysis.day') }}</span>
              11%
            </trend>
          </div>
          <template slot="footer">{{ $t('dashboard.analysis.day-sales') }}<span>12356人</span></template>
        </chart-card>
      </a-col>
      <a-col :sm="24" :md="12" :xl="6" :style="{ marginBottom: '24px' }">
        <chart-card :loading="loading" :title="$t('dashboard.analysis.visits')" :total="8846 | NumberFormat">
          <a-tooltip :title="$t('dashboard.analysis.introduce')" slot="action">
            <a-icon type="info-circle-o" />
          </a-tooltip>
          <div>
            <mini-area />
          </div>
          <template slot="footer">{{ $t('dashboard.analysis.day-visits') }}<span> {{ '1234' | NumberFormat }}</span></template>
        </chart-card>
      </a-col>
      <a-col :sm="24" :md="12" :xl="6" :style="{ marginBottom: '24px' }">
        <chart-card :loading="loading" :title="$t('dashboard.analysis.payments')" :total="6560 | NumberFormat">
          <a-tooltip :title="$t('dashboard.analysis.introduce')" slot="action">
            <a-icon type="info-circle-o" />
          </a-tooltip>
          <div>
            <mini-bar />
          </div>
          <template slot="footer">{{ $t('dashboard.analysis.conversion-rate') }} <span>60%</span></template>
        </chart-card>
      </a-col>
      <a-col :sm="24" :md="12" :xl="6" :style="{ marginBottom: '24px' }">
        <chart-card :loading="loading" :title="$t('dashboard.analysis.operational-effect')" total="预计排队3分钟">
          <a-tooltip :title="$t('dashboard.analysis.introduce')" slot="action">
            <a-icon type="info-circle-o" />
          </a-tooltip>
          <div>
            <mini-progress color="rgb(19, 194, 194)" :target="80" :percentage="78" height="8px" />
          </div>
          <template slot="footer">
            <trend flag="down" style="margin-right: 16px;">
              <span slot="term">{{ $t('dashboard.analysis.week') }}</span>
              12%
            </trend>
            <trend flag="up">
              <span slot="term">{{ $t('dashboard.analysis.day') }}</span>
              80%
            </trend>
          </template>
        </chart-card>
      </a-col>
    </a-row>

    <a-card :loading="loading" :bordered="false" :body-style="{padding: '0'}">
      <div class="salesCard">
        <a-tabs default-active-key="1" size="large" :tab-bar-style="{marginBottom: '24px', paddingLeft: '16px'}">
          <div class="extra-wrapper" slot="tabBarExtraContent">
            <div class="extra-item">
              <a>{{ $t('dashboard.analysis.all-day') }}</a>
              <a>{{ $t('dashboard.analysis.all-week') }}</a>
              <a>{{ $t('dashboard.analysis.all-month') }}</a>
              <a>{{ $t('dashboard.analysis.all-year') }}</a>
            </div>
            <a-range-picker :style="{width: '256px'}" />
          </div>
          <a-tab-pane loading="true" :tab="$t('dashboard.analysis.sales')" key="1">
            <a-row>
              <a-col :xl="16" :lg="12" :md="12" :sm="24" :xs="24">
                <bar :data="barData" :title="$t('dashboard.analysis.sales-trend')" />
              </a-col>
              <a-col :xl="8" :lg="12" :md="12" :sm="24" :xs="24">
                <rank-list :title="$t('dashboard.analysis.sales-ranking')" :list="rankList"/>
              </a-col>
            </a-row>
          </a-tab-pane>
          <a-tab-pane :tab="$t('dashboard.analysis.visits')" key="2">
            <a-row>
              <a-col :xl="16" :lg="12" :md="12" :sm="24" :xs="24">
                <bar :data="barData2" :title="$t('dashboard.analysis.visits-trend')" />
              </a-col>
              <a-col :xl="8" :lg="12" :md="12" :sm="24" :xs="24">
                <rank-list :title="$t('dashboard.analysis.visits-ranking')" :list="rankList"/>
              </a-col>
            </a-row>
          </a-tab-pane>
        </a-tabs>
      </div>
    </a-card>

    <div :class="!isMobile && 'desktop'">
      <a-row :gutter="24" type="flex" :style="{ marginTop: '24px', alignItems: 'stretch' }">
        <!-- 第一列 -->
        <a-col :sm="48" :md="24" :xl="12" style="display: flex; flex-direction: column; height: 100%">
          <a-card :loading="loading" :bordered="false" :title="$t('dashboard.analysis.online-top-search')" :style="{ flex: 1, height: '100%' }">
            <a-dropdown :trigger="['click']" placement="bottomLeft" slot="extra">
              <a class="ant-dropdown-link" href="#">
                <a-icon type="ellipsis" />
              </a>
              <a-menu slot="overlay">
                <a-menu-item>
                  <a href="javascript:;">{{ $t('dashboard.analysis.dropdown-option-one') }}</a>
                </a-menu-item>
                <a-menu-item>
                  <a href="javascript:;">{{ $t('dashboard.analysis.dropdown-option-two') }}</a>
                </a-menu-item>
              </a-menu>
            </a-dropdown>
            <a-row :gutter="68">
              <a-col :xs="24" :sm="12" :style="{ marginBottom: '24px'}">
                <number-info :total="185271" :sub-total="17.1">
                  <span slot="subtitle">
                    <span>{{ $t('dashboard.analysis.search-users') }}</span>
                    <a-tooltip :title="$t('dashboard.analysis.introduce')" slot="action">
                      <a-icon type="info-circle-o" :style="{ marginLeft: '8px' }" />
                    </a-tooltip>
                  </span>
                </number-info>
                <!-- miniChart -->
                <div>
                  <mini-smooth-area :style="{ height: '45px' }" :dataSource="searchUserData" :scale="searchUserScale" />
                </div>
              </a-col>
              <a-col :xs="24" :sm="12" :style="{ marginBottom: '24px'}">
                <number-info :total="18900" :sub-total="26.2" status="down">
                  <span slot="subtitle">
                    <span>{{ $t('dashboard.analysis.per-capita-search') }}</span>
                    <a-tooltip :title="$t('dashboard.analysis.introduce')" slot="action">
                      <a-icon type="info-circle-o" :style="{ marginLeft: '8px' }" />
                    </a-tooltip>
                  </span>
                </number-info>
                <div>
                  <mini-smooth-area :style="{ height: '45px' }" :dataSource="searchUserData" :scale="searchUserScale" />
                </div>
              </a-col>
            </a-row>
            <div class="ant-table-wrapper">
              <a-table
                row-key="index"
                size="small"
                :columns="searchTableColumns"
                :dataSource="searchData"
                :pagination="{ pageSize: 5 }"
              >
                <span slot="range" slot-scope="text, record">
                  <trend :flag="record.status === 0 ? 'up' : 'down'">
                    {{ text }}%
                  </trend>
                </span>
              </a-table>
            </div>
          </a-card>
        </a-col>

        <!-- 第二列 -->
        <a-col :sm="24" :md="12" :xl="6" style="display: flex; flex-direction: column; height: 100%">
          <a-card
            title="安检指数"
            style="margin-bottom: 24px;font-weight: 100;"
            :loading="radarLoading"
            :bordered="false"
            :body-style="{ padding: 0 }"
          >
            <div style="min-height: 400px;font-family:'Microsoft YaHei';">
              <h4 style="margin: 20px;">{{ $t('dashboard.analysis.s5') }}</h4>
              <!-- :scale="scale" :axis1Opts="axis1Opts" :axis2Opts="axis2Opts"  -->
              <radar :data="radarData" />
            </div>
          </a-card>
        </a-col>

        <!-- 第三列 -->
        <a-col :sm="24" :md="12" :xl="6" style="display: flex; flex-direction: column; height: 100%">
          <a-card class="antd-pro-pages-dashboard-analysis-salesCard" :loading="loading" :bordered="false" :title="$t('dashboard.analysis.the-proportion-of-sales')" :style="{ flex: 1, height: '100%' }">
            <div slot="extra" style="height: inherit;">
              <span class="dashboard-analysis-iconGroup">
                <a-dropdown :trigger="['click']" placement="bottomLeft">
                  <a-icon type="ellipsis" class="ant-dropdown-link" />
                  <a-menu slot="overlay">
                    <a-menu-item>
                      <a href="javascript:;">{{ $t('dashboard.analysis.dropdown-option-one') }}</a>
                    </a-menu-item>
                    <a-menu-item>
                      <a href="javascript:;">{{ $t('dashboard.analysis.dropdown-option-two') }}</a>
                    </a-menu-item>
                  </a-menu>
                </a-dropdown>
              </span>
              <div class="analysis-salesTypeRadio">
                <a-radio-group defaultValue="a" style="align-self: center;" size="small">
                  <a-radio-button value="a" >{{ $t('dashboard.analysis.channel.all') }}</a-radio-button>
                  <a-radio-button value="b" >{{ $t('dashboard.analysis.channel.online') }}</a-radio-button>
                  <a-radio-button value="c" >{{ $t('dashboard.analysis.channel.stores') }}</a-radio-button>
                </a-radio-group>
              </div>
            </div>
            <h4>{{ $t('dashboard.analysis.sales') }}</h4>
            <div>
              <v-chart :force-fit="true" :height="405" :data="pieData" :scale="pieScale">
                <v-tooltip :showTitle="false" dataKey="item*percent" />
                <v-axis />
                <v-legend dataKey="item"/>
                <v-pie position="percent" color="item" :vStyle="pieStyle" />
                <v-coord type="theta" :radius="0.75" :innerRadius="0.6" />
              </v-chart>
            </div>
          </a-card>
        </a-col>
      </a-row>

    </div>

    <!-- 添加雷达图和扇形图的 div 元素 -->
    <!-- <a-row :gutter="24" type="flex" :style="{ marginTop: '24px' }">
      <a-col :xl="12" :lg="12" :md="24" :sm="24" :xs="24">
        <div ref="radarChart" style="width: 100%; height: 400px;"></div>
      </a-col>
      <a-col :xl="12" :lg="12" :md="24" :sm="24" :xs="24">
        <div ref="pieChart" style="width: 100%; height: 400px;"></div>
      </a-col>
    </a-row> -->
  </div>
</template>

<script>
import moment from 'moment'

// import * as echarts from 'echarts'
import {
  ChartCard,
  MiniArea,
  MiniBar,
  MiniProgress,
  RankList,
  Bar,
  Trend,
  NumberInfo,
  MiniSmoothArea,
  Radar
} from '@/components'
import { baseMixin } from '@/store/app-mixin'

const barData = []
const barData2 = []
for (let i = 0; i < 12; i += 1) {
  barData.push({
    x: `${i + 1}月`,
    y: Math.floor(Math.random() * 1000) + 200
  })
  barData2.push({
    x: `${i + 1}月`,
    y: Math.floor(Math.random() * 1000) + 200
  })
}

const rankList = []
const cities = ['杭州市', '宁波市', '温州市', '嘉兴市', '湖州市', '绍兴市', '金华市']
for (let i = 0; i < cities.length; i++) {
  rankList.push({
    name: cities[i],
    total: 12340056 - i * 1000
  })
}

const searchUserData = []
for (let i = 0; i < 7; i++) {
  searchUserData.push({
    x: moment().add(i, 'days').format('YYYY-MM-DD'),
    y: Math.ceil(Math.random() * 10)
  })
}
const searchUserScale = [
  {
    dataKey: 'x',
    alias: '时间'
  },
  {
    dataKey: 'y',
    alias: '用户数',
    min: 0,
    max: 10
  }]

const searchData = []
const keywords = ['打火机', '酒精', '刀具', '易燃物', '毒品', '枪支', '爆炸物']
for (let i = 0; i < keywords.length; i++) {
  searchData.push({
    index: i + 1,
    keyword: keywords[i],
    count: Math.floor(Math.random() * 1000),
    range: Math.floor(Math.random() * 100),
    status: Math.floor((Math.random() * 10) % 2)
  })
}

const DataSet = require('@antv/data-set')

const sourceData = [
  { item: '酒精', count: 32.2 },
  { item: '打火机', count: 21 },
  { item: '管制刀具', count: 17 },
  { item: '肥料', count: 13 },
  { item: '毒品', count: 9 },
  { item: '其他', count: 7.8 }
]

const pieScale = [{
  dataKey: 'percent',
  min: 0,
  formatter: '.0%'
}]

const dv = new DataSet.View().source(sourceData)
dv.transform({
  type: 'percent',
  field: 'count',
  dimension: 'item',
  as: 'percent'
})
const pieData = dv.rows

export default {
  name: 'Analysis',
  mixins: [baseMixin],
  components: {
    ChartCard,
    MiniArea,
    MiniBar,
    MiniProgress,
    RankList,
    Radar,
    Bar,
    Trend,
    NumberInfo,
    MiniSmoothArea
  },
  data () {
    return {
      loading: true,
      rankList,
      radarLoading: true,
      // 搜索用户数
      searchUserData,
      searchUserScale,
      searchData,
      radarData: [],
      barData,
      barData2,

      //
      pieScale,
      pieData,
      sourceData,
      pieStyle: {
        stroke: '#fff',
        lineWidth: 1
      }
    }
  },
  computed: {
    searchTableColumns () {
        return [
      {
        dataIndex: 'index',
        title: this.$t('dashboard.analysis.table.rank'),
        width: 90
      },
      {
        dataIndex: 'keyword',
        title: this.$t('dashboard.analysis.table.search-keyword')
      },
      {
        dataIndex: 'count',
        title: this.$t('dashboard.analysis.table.users')
      },
      {
        dataIndex: 'range',
        title: this.$t('dashboard.analysis.table.weekly-range'),
        align: 'right',
        sorter: (a, b) => a.range - b.range,
        scopedSlots: { customRender: 'range' }
      }
      ]
    }
  },
  mounted () {
    this.initRadar()
    this.handleResize()// 初次加载时调整大小
    window.addEventListener('resize', this.handleResize) // 添加resize事件监听
  },
  beforeDestroy () {
    window.removeEventListener('resize', this.handleResize) // 销毁前移除事件监听
  },
  methods: {
    handleResize () {
      const cardContainer = this.$refs.cardContainer
      const radarChart = this.$refs.radarChart

      const containerWidth = cardContainer.offsetWidth
      const chartWidth = Math.min(containerWidth * 0.8, 600) // 设置最大宽度
      radarChart.style.width = `${chartWidth}px` // 根据卡片宽度调整图表宽度
    },
    initRadar () {
  this.radarLoading = true

  this.$http.get('/workplace/radar').then(res => {
    if (res.result && res.result.length > 0) { // 确保有数据
      const dv = new DataSet.View().source(res.result)
      dv.transform({
        type: 'fold',
        fields: ['个人', '团队', '部门'], // 确保你的字段正确
        key: 'user',
        value: 'score'
      })
      this.radarData = dv.rows
    } else {
      console.warn('雷达数据为空:', res)
    }
    this.radarLoading = false
  }).catch(err => {
    console.error('获取雷达数据失败:', err)
    this.radarLoading = false
  })
}

  },
  created () {
    setTimeout(() => {
      this.loading = !this.loading
    }, 1000)
  }
}
</script>

  <style lang="less" scoped>
.extra-wrapper {
  line-height: 55px;
  padding-right: 24px;

  .extra-item {
    display: inline-block;
    margin-right: 24px;

    a {
      margin-left: 24px;
    }
  }
}

.antd-pro-pages-dashboard-analysis-twoColLayout {
  position: relative;
  display: flex;
  flex-flow: row wrap;
}

.antd-pro-pages-dashboard-analysis-salesCard {
  height: calc(100% - 24px);
  /deep/ .ant-card-head {
    position: relative;
  }
}

.dashboard-analysis-iconGroup {
  i {
    margin-left: 16px;
    color: rgba(0,0,0,.45);
    cursor: pointer;
    transition: color .32s;
  }
}

.analysis-salesTypeRadio {
  position: absolute;
  left:130px;
  bottom: 16px;
  align-self: center;
}
</style>
