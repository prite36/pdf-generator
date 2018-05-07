<template>
  <div class="hello">
    <button @click="createPDF()">Download</button>
  </div>
</template>

<script>
import logoHeader from '../assets/FITM_LOGO.png'
import pdfMake from 'pdfmake/build/pdfmake'
import pdfFonts from 'pdfmake/build/vfs_fonts'
import momentTime from 'moment-timezone'
pdfMake.vfs = pdfFonts.pdfMake.vfs
pdfMake.fonts = {
  THSarabunNew: {
    normal: 'THSarabunNew.ttf',
    bold: 'THSarabunNew-Bold.ttf',
    italics: 'THSarabunNew-Italic.ttf',
    bolditalics: 'THSarabunNew-BoldItalic.ttf'
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
      var docDefinition = {
        pageMargins: [40, 120, 40, 40],
        header: () => {
          return [{
            style: 'headerPage',
            table: {
              widths: ['auto', 200, 230],
              body: [
                [
                  {
                    image: logoHeader,
                    width: 60,
                    border: [false, false, false, false]
                  },
                  {text: 'FITM Co-working space System', bold: true, border: [false, false, false, false]},
                  {
                    stack: [
                      {text: 'Report Statistics ', bold: true, alignment: 'right'},
                      {text: 'รายงานสถิติ ', bold: true, alignment: 'right'}
                    ],
                    border: [false, false, false, false]
                  }
                ]
              ]
            }
          },
          {
            canvas: [
              {
                type: 'line',
                x1: 40,
                y1: 20,
                x2: 595 - 40,
                y2: 20,
                lineWidth: 1
              }
            ]
          }]
        },
        footer: (currentPage, pageCount) => {
          return [{
            style: 'footerPage',
            text: `${momentTime().tz('Asia/Bangkok').format('วันที่  DD-MM-YYYY  เวลา  HH:mm')}\t\t\t\t\t\t\t\t Page ${currentPage.toString()}  of  ${pageCount}`
          }]
        },
        content: [
          {
            style: 'tableExample',
            table: {
              heights: 30,
              width: '*',
              headerRows: 1,
              body: [
                [{text: 'ประเภทห้อง\ntypeRoom', style: 'tableHeader'}, {text: 'เข้าใช้งาน\ncheck-in', style: 'tableHeader'}, {text: 'Header 3', style: 'tableHeader'}, {text: 'Header 4', style: 'tableHeader'}],
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
        defaultStyle: {
          font: 'THSarabunNew'
        },
        styles: {
          headerPage: {
            margin: [40, 20, 40, 0],
            fontSize: 16
          },
          footerPage: {
            margin: [40, 10, 40, 0],
            alignment: 'left',
            fontSize: 14
          },
          tableExample: {
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
