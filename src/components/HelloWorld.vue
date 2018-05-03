<template>
  <div class="hello">
    <button @click="createPDF()">Download</button>
  </div>
</template>

<script>
import pdfMake from 'pdfmake/build/pdfmake'
import pdfFonts from 'pdfmake/build/vfs_fonts'
pdfMake.vfs = pdfFonts.pdfMake.vfs
pdfMake.fonts = {
  THSarabunNew: {
    normal: 'THSarabunNew.ttf',
    bold: 'THSarabunNew-Bold.ttf',
    italics: 'THSarabunNew-Italic.ttf',
    bolditalics: 'THSarabunNew-BoldItalic.ttf'
  },
  Roboto: {
    normal: 'Roboto-Regular.ttf',
    bold: 'Roboto-Medium.ttf',
    italics: 'Roboto-Italic.ttf',
    bolditalics: 'Roboto-MediumItalic.ttf'
  }
}
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods: {
    createPDF () {
      // var win = window.open()
      // win.document.open()
      /* var docDefinition2 = {
        content: [
          {
            style: 'tableExample',
            table: {
              heights: 60,
              // widths: [ '*', 'auto', 100, '*' ],
              body: [
                [{text: 'Header 1', style: 'tableHeader'}, {text: 'Header 2', style: 'tableHeader'}, {text: 'Header 3', style: 'tableHeader'}, {text: 'Header 4', style: 'tableHeader'}],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
              ]
            }
          }
        ],
        styles: {
          tableExample: {
          margin: [0, 5, 0, 15]
          },
            tableHeader: {
            bold: true,
            fontSize: 14,
            color: 'black'
          }
        }
      } */
      var docDefinition = {
        footer: function (currentPage, pageCount) { return currentPage.toString() + ' of ' + pageCount },
        header: function (currentPage, pageCount, pageSize) {
          // you can apply any logic and return any valid pdfmake element
          return [
            { text: 'simple text', alignment: (currentPage % 2) ? 'left' : 'right' },
            { canvas: [ { type: 'rect', x: 170, y: 32, w: pageSize.width - 170, h: 40 } ] }
          ]
        },
        content: [
          {
            style: 'tableExample',
            table: {
              heights: 60,
              // widths: [ '*', 'auto', 100, '*' ],
              body: [
                [{text: 'Header 1', style: 'tableHeader'}, {text: 'Header 2', style: 'tableHeader'}, {text: 'Header 3', style: 'tableHeader'}, {text: 'Header 4', style: 'tableHeader'}],
                [ 'สวัสดดี', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ],
                [ 'Value 1', 'Value 2', 'Value 3', 'Value 4' ]
              ]
            }
          }
        ],
        defaultStyle:{
          font: 'THSarabunNew'
        },
        styles: {
          tableExample: {
            margin: [5, 5, 0, 15],
            fontSize: 14
          },
          tableHeader: {
            bold: true,
            fontSize: 16,
            color: 'black'
          }
        }
      }
      const pdfDocGenerator = pdfMake.createPdf(docDefinition)
      pdfDocGenerator.getBase64((buffer) => {
        var iframe = "<iframe width='100%' height='100%' src='data:application/pdf;base64," + buffer + "'></iframe>" // eslint-disable-line
        var x = window.open()
        x.document.open()
        x.document.write(iframe)
        x.document.close()
      })
      // pdfMake.createPdf(docDefinition).open({}, win)
    }
  },
  mounted () {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
table, td, th {
  border: 1px solid black;
  border-collapse: collapse;
}
</style>
