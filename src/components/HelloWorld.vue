<template>
  <div class="hello">
    <button @click="createPDF()">Download</button>
    <button @click="test()">test</button>
  </div>
</template>

<script>
import logoHeader from '../assets/FITM_LOGO.png'
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
      var docDefinition = {
        pageMargins: [40, 120, 40, 60],
        header: {
          style: 'headerPage',
          // table: {
          //   body: [
          //     ['Column 1', 'Column 2', 'Column 3'],
          //     ['One value goes here', 'Another one here', 'OK?']
          //   ]
          // },
          image: logoHeader
        },
        footer: (currentPage, pageCount) => {
          return {
            alignment: 'center',
            fontSize: 14,
            text: `Page ${currentPage.toString()}  of  ${pageCount}`
          }
        },
        content: [
          {
            style: 'tableExample',
            table: {
              heights: 60,
              // widths: [ '*', 'auto', 100, '*' ],
              headerRows: 1,
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
        defaultStyle: {
          font: 'THSarabunNew'
        },
        styles: {
          headerPage: {
            widths: ['auto', '*', '*'],
            margin: [40, 20, 40, 0]
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
