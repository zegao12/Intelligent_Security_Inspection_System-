<template>
  <div>
    <a-row :gutter="24" style="display: flex; flex-wrap: wrap;">
      <a-col :sm="24" :md="12" :xl="6" :style="{ marginBottom: '24px', display: 'flex', flexDirection: 'column' }">
        <chart-card :loading="loading" :title="$t('dashboard.analysis.total-sales')" total="126,560件" style="flex: 1;">
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
          <template slot="footer">{{ $t('dashboard.analysis.day-sales') }}<span>1234件</span></template>
        </chart-card>
      </a-col>

      <a-col :sm="24" :md="12" :xl="6" :style="{ marginBottom: '24px', display: 'flex', flexDirection: 'column' }">
        <chart-card :loading="loading" :title="$t('dashboard.analysis.visits')" :total="8846 | NumberFormat" style="flex: 1;">
          <a-tooltip :title="$t('dashboard.analysis.introduce')" slot="action">
            <a-icon type="info-circle-o" />
          </a-tooltip>
          <div>
            <mini-area />
          </div>
          <template slot="footer">{{ $t('dashboard.analysis.day-visits') }}<span> {{ '1234' | NumberFormat }}</span></template>
        </chart-card>
      </a-col>

      <a-col :sm="24" :md="12" :xl="6" :style="{ marginBottom: '24px', display: 'flex', flexDirection: 'column' }">
        <chart-card :loading="loading" :title="$t('dashboard.analysis.payments')" :total="6560 | NumberFormat" style="flex: 1;">
          <a-tooltip :title="$t('dashboard.analysis.introduce')" slot="action">
            <a-icon type="info-circle-o" />
          </a-tooltip>
          <div>
            <mini-bar />
          </div>
          <template slot="footer">{{ $t('dashboard.analysis.conversion-rate') }} <span>60%</span></template>
        </chart-card>
      </a-col>

      <a-col :sm="24" :md="12" :xl="6" :style="{ marginBottom: '24px', display: 'flex', flexDirection: 'column' }">
        <chart-card :loading="loading" :title="$t('dashboard.analysis.operational-effect')" total="预计排队3分钟" style="flex: 1;">
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

    <a-row :gutter="24" style="display: flex; flex-wrap: wrap;">
      <a-col :sm="48" :md="24" :xl="12" :style="{ marginBottom: '24px', display: 'flex', flexDirection: 'column' }">
        <a-card hoverable style="width: 100%; flex: 1;">
          <template #cover>
            <a-card-meta title="安检画面" style="margin: 25px;" />
            <img alt="example" src="@/img/微信截图_20250301143628.png" />
          </template>
        </a-card>
      </a-col>

      <a-col :sm="24" :md="12" :xl="6" :style="{ marginBottom: '24px', display: 'flex', flexDirection: 'column' }">
        <a-card hoverable style="width: 100%; flex: 1;">
          <template #cover>
            <a-card-meta title="检出物图像" style="margin: 25px;" />
            <img alt="example" src="@/img/微信截图_20250301150243.png" />
          </template>
        </a-card>
      </a-col>

      <a-col :sm="24" :md="12" :xl="6" :style="{ marginBottom: '24px' }">
        <a-card class="antd-pro-pages-dashboard-analysis-salesCard" :loading="loading" :bordered="false" :title="$t('dashboard.analysis.the-proportion-of-sales')">
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
          </div>

          <div class="chart-container">
            <v-chart :force-fit="true" :height="300" :data="pieData" :scale="pieScale">
              <v-tooltip :showTitle="false" dataKey="item*percent" />
              <v-axis />
              <v-legend dataKey="item"/>
              <v-pie position="percent" color="item" :vStyle="pieStyle" />
              <v-coord type="theta" :radius="1" :innerRadius="0.5" />
            </v-chart>
          </div>
        </a-card>
      </a-col>
    </a-row>

    <a-row :gutter="24">
      <a-col :sm="48" :md="24" :xl="12" :style="{ marginBottom: '24px' }">
        <div :style="{ background: 'rgb(255, 255, 255)', padding: '16px 16px', height: '60px', display: 'flex', justifyContent: 'center', alignItems: 'center' }">
          <a-space direction="horizontal" style="width: 100%; justify-content: center;">
            <a-button type="primary" danger ghost size="small" style="display: flex; align-items: center;font-size: 12px;background: rgb(245,245,245) !important;color: rgb(217,217,217);border-color: rgb(217,217,217)">
              <svg width="16" viewBox="0 0 48 48" fill="none" style="margin-right:10px;"><path d="M16 39.513l15.556-15.557L16 8.4" stroke="rgb(217,217,217)" stroke-width="2"/></svg>
              开始安检
            </a-button>
            <a-button type="primary" danger ghost size="small" style="display: flex; align-items: center;font-size: 12px;">
              <svg width="16" viewBox="0 0 48 48" fill="none" style="margin-right:10px"><path d="M42 24c0 9.941-8.059 18-18 18S6 33.941 6 24 14.059 6 24 6s18 8.059 18 18z" stroke="rgb(64,159,255)" stroke-width="2"/><path d="M19 19v10h1V19h-1zM28 19v10h1V19h-1z" stroke="#4E5969" stroke-width="2"/></svg>
              暂停画面
            </a-button>
            <a-button type="primary" danger ghost size="small" style="display: flex; align-items: center;font-size: 12px;">
              <svg width="16" viewBox="0 0 48 48" fill="none" style="margin-right:10px"><path d="M5 24h38M24 5v38" stroke="rgb(64,159,255)" stroke-width="2"/></svg>
              放大画面
            </a-button>
            <a-button type="primary" danger ghost size="small" style="display: flex; align-items: center;font-size: 12px;">
              <svg width="16" viewBox="0 0 48 48" fill="none" style="margin-right:10px"><path d="M5 24h38" stroke="rgb(64,159,255)" stroke-width="2"/></svg>
              缩小画面
            </a-button>
            <a-button type="primary" danger ghost size="small" style="display: flex; align-items: center;font-size: 12px;">
              <svg width="16" viewBox="0 0 48 48" fill="none" style="margin-right:10px"><path d="M11.27 20.272L23.998 7.544l12.728 12.728M24 43V8.705" stroke="rgb(64,159,255)" stroke-width="2"/></svg>
              图片增强与超分
            </a-button>
            <a-button type="primary" danger ghost size="small" style="display: flex; align-items: center;font-size: 12px;border-color: red;color: red;">
              <svg width="16" viewBox="0 0 48 48" fill="none" style="margin-right:10px"><path d="M36.728 11.272c7.03 7.03 7.03 18.427 0 25.456-7.03 7.03-18.427 7.03-25.456 0-7.03-7.03-7.03-18.427 0-25.456 7.03-7.03 18.427-7.03 25.456 0zM36.728 36.728L11.272 11.272" stroke="red" stroke-width="2"/></svg>
              停止安检
            </a-button>
          </a-space>
        </div>
      </a-col>
      <!-- <a-col :style="{ height: '24px' }"></a-col> -->
      <a-col :sm="48" :md="24" :xl="12" :style="{ marginBottom: '24px' }">
        <div :style="{ background: 'rgb(255, 255, 255)', padding: '16px 16px', height: '60px', display: 'flex', justifyContent: 'center', alignItems: 'center' }">
          <a-space direction="horizontal" style="width: 100%; justify-content: center;">
            <a-button type="primary" danger ghost size="small" style="display: flex; align-items: center;font-size: 12px;background: rgb(245,245,245) !important;color: rgb(217,217,217);border-color: rgb(217,217,217)">
              <svg width="16" viewBox="0 0 48 48" fill="none" style="margin-right: 10px;"><path d="M40 35v6H8v-6M14.93 17.071L24.001 8l9.071 9.071M24.002 33.142v-25" stroke="#4E5969" stroke-width="2"/></svg>
              危险物品上报
            </a-button>
            <a-button type="primary" danger ghost size="small" style="display: flex; align-items: center;font-size: 12px;">
              <svg width="16" viewBox="0 0 48 48" fill="none" style="margin-right:10px"><path d="M9 33.953C12.225 38.803 17.74 42 24 42c9.941 0 18-8.059 18-18S33.941 6 24 6C14.313 6 6.413 13.653 6.016 23.243c-.01.25-.016.503-.016.757" stroke="rgb(64,159,255)" stroke-width="2"/><path d="M32 26h-9v-9M5.5 23.243L6 24l.5-.757h-1z" stroke="#4E5969" stroke-width="2"/></svg>
              查看历史记录
            </a-button>
            <a-button type="primary" danger ghost size="small" style="display: flex; align-items: center;font-size: 12px;background: rgb(245,245,245) !important;color: rgb(217,217,217);border-color: rgb(217,217,217)">
              <svg width="16" viewBox="0 0 48 48" fill="none" style="margin-right:10px"><path d="M36.728 11.272c7.03 7.03 7.03 18.427 0 25.456-7.03 7.03-18.427 7.03-25.456 0-7.03-7.03-7.03-18.427 0-25.456 7.03-7.03 18.427-7.03 25.456 0zM36.728 36.728L11.272 11.272" stroke="#4E5969" stroke-width="2"/></svg>
              停止警报
            </a-button>
            <a-button type="primary" danger ghost size="small" style="display: flex; align-items: center;font-size: 12px;">
              <svg width="16" viewBox="0 0 48 48" fill="none" style="margin-right:10px"><path d="M13 24h30M5 11h4m4 26h30M13 11h30M5 24h4M5 37h4" stroke="rgb(64,159,255)" stroke-width="2"/></svg>
              危险等级自定义
            </a-button>
            <a-button type="primary" danger ghost size="small" style="display: flex; align-items: center;font-size: 12px;">
              <svg width="16" viewBox="0 0 48 48" fill="none" style="margin-right:10px"><path d="M43 22c0-7.732-6.492-14-14.5-14S14 14.268 14 22v.055A9.001 9.001 0 0015 40h13" stroke="rgb(64,159,255)" stroke-width="2"/><path d="M44.142 34.071l-7.07 7.071L30 34.071M37.07 26v15" stroke="#4E5969" stroke-width="2"/></svg>
              升级AI模型
            </a-button>
          </a-space>
        </div>
      </a-col>

    </a-row>
  </div>

</template>

    <script>
    import moment from 'moment'
    import CardItem from '@/components/mycomponent/CardItem'

    import {

      ChartCard,
      MiniArea,
      MiniBar,
      MiniProgress,
      RankList,
      Bar,
      Trend,
      NumberInfo,
      MiniSmoothArea
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
    for (let i = 0; i < 7; i++) {
      rankList.push({
        name: '白鹭岛 ' + (i + 1) + ' 号店',
        total: 1234.56 - i * 100
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
    for (let i = 0; i < 50; i += 1) {
      searchData.push({
        index: i + 1,
        keyword: `搜索关键词-${i}`,
        count: Math.floor(Math.random() * 1000),
        range: Math.floor(Math.random() * 100),
        status: Math.floor((Math.random() * 10) % 2)
      })
    }

    const DataSet = require('@antv/data-set')

    const sourceData = [
      { item: '安全物品', count: 79.8 },
      { item: '危险刀具', count: 20.2 }
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
        CardItem,
        ChartCard,
        MiniArea,
        MiniBar,
        MiniProgress,
        RankList,
        Bar,
        Trend,
        NumberInfo,
        MiniSmoothArea
      },
      data () {
        return {
          loading: true,
          rankList,
          cardData: [
        {
          title: '安检画面',
          imgsrc: 'https://th.bing.com/th/id/OIP.d2_oclpVd2RCJ3OrPcpskwHaIa?rs=1&pid=ImgDetMain'
        },
        {
          title: '检出物图像',
          imgsrc: 'https://newsimg.5054399.com/uploads/userup/1906/251635233331.jpg'
        },
        {
          title: '检出物分析',
          imgsrc: 'https://info.zufe.edu.cn/__local/6/C8/F4/0FF24071B470249DB40E8FA1E0F_EBCC09C4_45BD1.jpg'
        }
      ],
          // 搜索用户数
          searchUserData,
          searchUserScale,
          searchData,

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
      created () {
        setTimeout(() => {
          this.loading = !this.loading
        }, 1000)
      }
    }
    </script>

    <style lang="less" scoped>
     .card{
    display: flex;
    color: #56e619;
    padding: 10px;
  }
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
        display: block;
        flex-flow: row wrap;
      }
      .chart-container {
  display: flex;
  justify-content: center; /* 水平居中 */
  align-items: center;     /* 垂直居中 */
  height: 300px;          /* 设置容器高度 */
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
          color: black;
        }
      }
      .analysis-salesTypeRadio {
        position: absolute;
        right: 54px;
        bottom: 12px;
      }
    </style>
