<template>
  <div class="sample">
    <v-row>
      <v-col cols=7>
        <div class="ControllPanel">
          <h2 class="ControllPanel__mainHeading">レポートサンプルだよ</h2>
          <div class="ControllPanel__form">
            <v-form>
              <v-container>
                <v-row>
                  <v-text-field
                    v-model="subject"
                    :counter="50"
                    label="宛先"
                    required
                  ></v-text-field>
                </v-row>
                <v-row>
                  <v-text-field
                    v-model="title"
                    :counter="50"
                    label="タイトル"
                    required
                  ></v-text-field>
                </v-row>
                <v-row>
                  <v-label>テーマカラー</v-label>
                </v-row>
                <v-row :style='{"margin": "20px 0px"}'>
                  <v-color-picker v-model="themeColor"></v-color-picker>
                </v-row>
                <v-row>
                  <v-combobox
                    v-model="labels"
                    @change=setLabelToGraph
                    hide-selected
                      label="要素追加"
                    multiple
                    persistent-hint
                    small-chips
                  >
                    <template v-slot:no-data>
                      <v-list-item>
                        <v-list-item-content>
                          <v-list-item-title>
                           <kbd>enter</kbd>  を押して要素を追加
                          </v-list-item-title>
                        </v-list-item-content>
                      </v-list-item>
                    </template>
                  </v-combobox>
                </v-row>
                <v-row>
                  <v-text-field
                    v-model="sampleDataCountA"
                    label="サンプルデータAのデータ数"
                    required
                  ></v-text-field>
                </v-row>
                <v-row>
                  <v-text-field
                    v-model="sampleDataCountB"
                    label="サンプルデータBのデータ数"
                    required
                  ></v-text-field>
                </v-row>
              </v-container>
            </v-form>
          </div>
        </div>
      </v-col>
      <v-col cols=5>
        <div class="previewArea">
          <div class="previewArea__HTML">
            <div ref="content">
              <div class="report">
                <div class="report__container">
                  <hr class="report__border" :style='{"backgroundColor": themeColor}'>
                  <h3 class="report__date">提出日: 2020/02/07</h3>
                  <h3 class="report__subject">{{ subject }} 御中</h3>
                  <h1 class="report__title">{{ title }}</h1>

                  <div class="report__main">
                    <section>
                      <h2 class="report__headingMiddle">1. サマリー</h2>
                      <div class="report__summaryTables">
                        <div class="report__summaryTable">
                          <div></div>
                          <div>目 標</div>
                          <div>実 績</div>
                        </div>
                        <div class="report__summaryTable">
                          <div>成果件数</div>
                          <div><b>¥0</b></div>
                          <div><b>¥2,195,261</b></div>
                        </div>
                        <div class="report__summaryTable">
                          <div>成果件数</div>
                          <div><b>0</b></div>
                          <div><b>625</b></div>
                        </div>
                        <div class="report__summaryTable">
                          <div>成果単価</div>
                          <div><b>¥0</b></div>
                          <div><b>¥3,515</b></div>
                        </div>
                      </div>

                      <div class="report__graphs">
                        <div class="report__graph report__graph--bar">
                          <BarChart :chartData="barChartData" :options="barChartOption"/>
                        </div>
                        <div class="report__graph report__graph--chart">
                          <RadarChart :chartData="radarChartData" :options="radarChartOption"/>
                        </div>
                      </div>
                    </section>

                    <section>
                      <h2 class="report__headingMiddle">2. サンプルデータA</h2>
                      <div class="report__dataTables">
                        <table cellspacing="0" cellpadding="0">
                          <thead>
                            <tr>
                              <th>ラベル</th>
                              <th>年月</th>
                              <template v-for="(label, index) of labels">
                                <th :key="index">{{ label }}</th>
                              </template>
                            </tr>
                          </thead>
                          <tbody>
                            <template v-for="n of (Number(sampleDataCountA) < 50 ? Number(sampleDataCountA) : 50 )">
                              <tr :key="n">
                                <th :key="n" rowspan="3">データ{{ n }}</th>
                                <td :key="n">2018年1月</td>
                                <td v-for="(label, index) of labels" :key="index">
                                  <span :key="n">{{ dummyData() }}</span>
                                </td>
                              </tr>
                              <tr :key="n">
                                <td :key="n">2018年2月</td>
                                <td v-for="(label, index) of labels" :key="index">
                                  <span :key="n">{{ dummyData() }}</span>
                                </td>
                              </tr>
                              <tr :key="n">
                                <td :key="n">2018年3月</td>
                                <td v-for="(label, index) of labels" :key="index">
                                  <span :key="n">{{ dummyData() }}</span>
                                </td>
                              </tr>
                            </template>
                          </tbody>
                        </table>
                      </div>
                    </section>

                    <section>
                      <h2 class="report__headingMiddle">3. サンプルデータB</h2>
                      <div class="report__dataTables">
                        <table cellspacing="0" cellpadding="0">
                          <thead>
                            <tr>
                              <th>ラベル</th>
                              <th>年月</th>
                              <template v-for="(label, index) of labels">
                                <th :key="index">{{ label }}</th>
                              </template>
                            </tr>
                          </thead>
                          <tbody>
                            <template v-for="n of (Number(sampleDataCountB) < 50 ? Number(sampleDataCountB) : 50 )">
                              <tr :key="n">
                                <th :key="n" rowspan="3">データ{{ n }}</th>
                                <td :key="n">2018年1月</td>
                                <td v-for="(label, index) of labels" :key="index">
                                  <span :key="n">{{ dummyData() }}</span>
                                </td>
                              </tr>
                              <tr :key="n">
                                <td :key="n">2018年2月</td>
                                <td v-for="(label, index) of labels" :key="index">
                                  <span :key="n">{{ dummyData() }}</span>
                                </td>
                              </tr>
                              <tr :key="n">
                                <td :key="n">2018年3月</td>
                                <td v-for="(label, index) of labels" :key="index">
                                  <span :key="n">{{ dummyData() }}</span>
                                </td>
                              </tr>
                            </template>
                          </tbody>
                        </table>
                      </div>
                    </section>
                  </div>
                  <hr class="report__border" :style='{"backgroundColor": themeColor}'>
                </div>
              </div>
            </div>
          </div>
          <div class="previewArea__Image">
            <img :src="imageURL">
          </div>
          <div>
            <v-btn @click="save" class="saveButton" color="primary">PDFで保存</v-btn>
          </div>
        </div>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import html2canvas from 'html2canvas'
import jsPDF from 'jspdf'
import BarChart from './BarChart';
import RadarChart from './RadarChart';

export default {
  name: 'Sample',

  components: {
    BarChart,
    RadarChart,
  },

  data: function() {
    return {
      // for html2canvas
      // see: https://html2canvas.hertzen.com/configuration
      canvasOption: {
        'backgroundColor': '#ffffff',
        'scrollX': 0,
        'scrollY': 0,
        'width': 595,  // A4 サイズ
        'height': 841, // A4 サイズ
      },

      // for jsPDF
      // see: https://rawgit.com/MrRio/jsPDF/master/docs/jsPDF.html
      pdfOption: {
        'format': 'a4',
        'unit': 'px',
      },

      sampleData: [
        {name: "U.F.O.", rank: 1, point: 826},
        {name: "ペヤング", rank: 2, point: 673},
        {name: "一平ちゃん", rank: 3, point: 287},
        {name: "やきそば弁当", rank: 4, point: 198},
        {name: "焼そばバゴォーン", rank: 5, point: 91},
      ],

      subject: "株式会社 カップ焼きそば",
      title: "カップ焼きそば レポート",
      themeColor: "#3c8dbe",
      labels:  ["U.F.O.", "ペヤング", "一平ちゃん", "やきそば弁当", "ごつ盛り"],
      sampleDataCountA: 2,
      sampleDataCountB: 5,
      imageURL: "",

      barChartData: {
        labels: ["やきそば弁当", "U.F.O.", "ペヤング", "一平ちゃん", "ごつ盛り"],
        datasets: [{
          label: "点数",
          data: [98, 226, 145, 207, 291],
          borderColor: "#fc8675",
          order: 1,
        },
        {
          label: "得票数 (line)",
          data: [98, 226, 145, 207, 291],
          borderColor: "#fc8675",
          type: 'line',
          order: 2,
          tension: 0,
          fill: false,
        }],
      },
      barChartOption: {
        legend: {
          display: false,
        },
      },

      radarChartData: {
        labels: ["U.F.O.", "ペヤング", "一平ちゃん", "やきそば弁当", "ごつ盛り"],
        legend: {
          display: false,
        },
        datasets: [{
          data: [226, 173, 187, 128, 243],
          borderColor: "#fc8675",
        }],
      },
      radarChartOption: {
        legend: {
          display: false,
        },
      },
    }
  },
  props: {},
  mounted: function() {
    html2canvas(this.$refs.content, this.canvasOption).then((canvas) => {
      this.imageURL = canvas.toDataURL()
    })
  },
  methods: {
    "save": function() {
      let pdf = new jsPDF(this.pdfOption)
      let size = pdf.internal.pageSize
      html2canvas(this.$refs.content, this.canvasOption).then((canvas) => {
        pdf.addImage(canvas.toDataURL(), 'JPEG', 0, 0, size.getWidth(), size.getHeight())
        pdf.save('test.pdf')
      })
    },
    "dummyData": function() {
      return Math.floor(Math.random() * Math.floor(40000)) / 100;
    },
    "setLabelToGraph": function(labels) {
      // Bar 更新
      let barChartData = Object.assign({}, this.barChartData)
      barChartData.labels = labels
      barChartData.datasets.map((d) => {
        d.data = d.data.slice(0, labels.length)

        if (d.data.length < labels.length) {
          for (let i = 0; i < labels.length - d.data.length; i++) {
            d.data.push(this.dummyData())
          }
        }
      })
      this.barChartData = barChartData

      // Radar 更新
      let radarChartData = Object.assign({}, this.radarChartData)
      radarChartData.labels = labels
      radarChartData.datasets.map((d) => {
        d.data = d.data.slice(0, labels.length)

        if (d.data.length < labels.length) {
          for (let i = 0; i < labels.length - d.data.length; i++) {
            d.data.push(this.dummyData())
          }
        }
      })
      this.radarChartData = radarChartData
    }
  },
}
</script>

<style lang="scss">
  $a4_width: 595px;
  $a4_height: 841px;

  .sample {
    margin: 20px 30px;
  }

  .saveButton {
    position: fixed!important;
    right: 60px;
    bottom: 9%;
  }

  .previewArea {
    position: fixed;
    width: $a4_width;
    max-height: $a4_height;
    height: 100%;
    right: 30px;
    overflow: scroll;

    &__HTML {
      width: $a4_width;
      height: $a4_height;
      border: 0px solid #ccc;
      background-color: #fff;
      border-radius: 2px;
      position: absolute;
      right: 0;
      margin-bottom: 400px; // 下まで余裕を持ってスクロールできるようにする
    }

    &__Image {
      position: absolute;
      right: 0;
      width: 100%;
      img {
        width: 100%;
      }

      // HTML を確認する用
      display: none;
    }
  }

  .ControllPanel {
    &__form {
      margin: 20px 140px 20px 80px;
    }

    &__mainHeading {
      font-size: 16px;
      color: #686868;
    }
  }

  .report {
    // レポートはブラウザで対応できないサイズのフォントを扱うため、レポート全体を1/2に縮小しています
    // そのため .report 以下のスタイルは、実際の半分の大きさで描画されます
    transform: scale(0.5);

    &__container {
      padding: 40px;
      width: 200%;
      left: -50%;
      position: absolute;
    }

    &__title {
      font-size: 18px;
      text-align: center;
      margin: 40px 120px;
      padding: 5px 0;
      border-bottom: 2px solid;
    }

    &__main {
      padding: 0 30px;
    }

    &__subject, &__date {
      font-size: 12px;
      font-weight: normal;
      padding: 0 30px;
    }

    &__date {
      text-align: right;
    }

    &__border {
      height: 8px;
      background-color: #3c8dbe;
      border: 0;
      margin-bottom: 10px;
    }

    &__headingMiddle {
      font-size: 14px;
      background-color: #0b8043;
      color: #fff;
      padding: 4px 10px;
    }

    &__summaryTables {
      display: flex;
      justify-content: space-between;
      margin-top: 10px;
    }

    &__summaryTable {
      div {
        min-height: 45px;
        font-size: 15px;
        width: 200px;
        text-align: center;
        padding: 6px;
        border-bottom: 2px solid;
        display: flex;
        align-items: center;
        justify-content: center;
        b {
          font-size: 20px;
        }
      }
    }

    &__graphs {
      width: 100%;
      display: flex;
      margin: 40px 0;
      justify-content: space-around;
    }

    &__graph {
      &--bar {
        width: 260px;
        height: 260px;
      }
      &--chart {
        width: 260px;
        height: 260px;
      }
    }

    &__dataTables {
      margin: 20px 0 40px;
      table {
        width: 100%;
      }
      thead {
        th {
          font-weight: normal;
          border-top: 2px solid;
          border-bottom: 2px solid;
        }
      }
      tbody {
        td {
          text-align: right;
          padding-right: 20px;
        }
        th {
          font-weight: normal;
          border-bottom: 2px solid;
        }
        tr:nth-child(3n+1) {
          font-weight: bold;
        }
        tr:nth-child(3n) td {
          border-bottom: 2px solid;
        }
        tr:nth-child(odd) td {
          background-color: #99554411;
        }
      }
    }
  }


</style>
