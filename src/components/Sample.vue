<template>
  <div class="sample">
    <v-row>
      <v-col cols=6>
        <div ref="content" class="doc" style="width:300px">
          <p style="font-size:6px; text-align: center;">
          コンポーネントにダークテーマを適応します。詳しく知りたい場合は
          コンポーネントにダークテーマを適応します。詳しく知りたい場合は
          コンポーネントにダークテーマを適応します。詳しく知りたい場合は
          コンポーネントにダークテーマを適応します。詳しく知りたい場合は
        </p>
        </div>
      </v-col>
      <v-col cols=6>
        <div class="reportContainer">
          <div class="reportBox">
            <div ref="result" class="report"></div>
          </div>
        </div>
        <div>
          <v-btn @click="save" class="saveButton" color="primary">PDFで保存</v-btn>
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
      'canvasOption': {
        'backgroundColor': '#cfccdd',
        'width': 595,  // A4 サイズ
        'height': 841, // A4 サイズ
      },
      'pdfOption': {
        'format': 'a4',
        'unit': 'px',
      },
    }
  },
  props: {},
  mounted: function() {
    html2canvas(this.$refs.content, this.canvasOption).then((canvas) => {
      this.$refs.result.appendChild(canvas)
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

<style scoped>
  .sample {
    margin: 0 30px;
  }

  .reportContainer {
    position: fixed;
    width: 48%;
    height: 96%;
    right: 1%;
    overflow: scroll;
  }

  .reportBox {
    width: 100%;
  }

  .report {
    height: 950px;
    margin-bottom: 20px;
  }

  .saveButton {
    position: fixed;
    right: 20px;
    top: 730px;
  }

  .doc {
    border: 1px solid #ccc;
    background-color: #eee;
  }
</style>
