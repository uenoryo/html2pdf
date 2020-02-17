<template>
  <div class="sample">
    <v-row>
      <v-col cols=7>
        コントロールぱねる
      </v-col>
      <v-col cols=5>
        <div class="previewArea">
          <div class="previewArea__HTML">
            <div ref="content">
              コンポーネントにダークテーマを適応します。詳しく知りたい場合は
              コンポーネントにダークテーマを適応します。詳しく知りたい場合は
              コンポーネントにダークテーマを適応します。詳しく知りたい場合は
              コンポーネントにダークテーマを適応します。詳しく知りたい場合は
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
      imageURL: '',
      canvasOption: {
        'backgroundColor': '#cfccdd',
        'width': 595,  // A4 サイズ
        'height': 841, // A4 サイズ
      },
      pdfOption: {
        'format': 'a4',
        'unit': 'px',
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
  },
}
</script>

<style lang="scss">
  $a4_width: 595px;
  $a4_height: 841px;

  .sample {
    margin: 20px 30px;
  }

  .reportBox {
    width: 100%;
  }

  .saveButton {
    position: fixed!important;
    right: 60px;
    bottom: 9%;
  }

  .content {
    //
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
      background-color: #eee;
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
</style>
