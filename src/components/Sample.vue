<template>
  <div class="sample">
    <v-row>
      <v-col cols=7>
        コントロールぱねる
      </v-col>
      <v-col cols=5>
        <div class="previewArea">
          <div class="previewArea__HTML">
            <div ref="content" class="report">
              <hr class="report__border">
              <h3 class="report__date">提出日: 2020/02/07</h3>
              <h3 class="report__subject">株式会社カップ焼きそば 御中</h3>
              <h1 class="report__title">結局一番うまい「カップ焼きそば」ランキング</h1>

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
                </section>
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

export default {
  name: 'Sample',
  data: function() {
    return {
      // for html2canvas
      // see: https://html2canvas.hertzen.com/configuration
      canvasOption: {
        'backgroundColor': '#ffffff',
        'width': 595,  // A4 サイズ
        'height': 841, // A4 サイズ
      },

      // for jsPDF
      // see: https://rawgit.com/MrRio/jsPDF/master/docs/jsPDF.html
      pdfOption: {
        'format': 'a4',
        'unit': 'px',
      },

      // sample data
      // see: https://ranking.goo.ne.jp/column/6231/ranking/52356/
      sampleData: [
        {name: "U.F.O.", rank: 1, point: 826},
        {name: "ペヤング", rank: 2, point: 673},
        {name: "一平ちゃん", rank: 3, point: 287},
        {name: "やきそば弁当", rank: 4, point: 198},
        {name: "焼そばバゴォーン", rank: 5, point: 91},
      ],

      imageURL: '',
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


  .report {
    padding: 20px;
    &__title {
      font-size: 12px;
      text-align: center;
      margin: 30px 60px;
      padding: 5px 0;
      border-bottom: 1px solid;
    }

    &__main {
      padding: 0 15px;
    }

    &__subject, &__date {
      font-size: 10px;
      font-weight: normal;
      padding: 0 15px;
    }

    &__date {
      text-align: right;
    }

    &__border {
      height: 4px;
      background-color: #3c8dbe;
      border: 0;
      margin-bottom: 10px;
    }

    &__headingMiddle {
      font-size: 10px;
      background-color: #0b8043;
      color: #fff;
      padding: 2px 5px;
    }

    &__summaryTables {
      display: flex;
      justify-content: space-between;
      margin-top: 10px;
    }

    &__summaryTable {
      div {
        min-height: 30px;
        font-size: 6px;
        width: 100px;
        text-align: center;
        padding: 6px;
        border-bottom: 1px solid;
      }
    }
  }

</style>
