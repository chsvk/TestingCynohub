<template>
  <ion-page>
    <ion-content :fullscreen="true">
         <div id="pageContainer">
            <div id="viewer" class="pdfViewer"></div>     
          </div>
    </ion-content>
  </ion-page>
</template>

<script>

import { IonPage, IonContent } from '@ionic/vue';
import pdfjsLib from "pdfjs-dist/build/pdf";
import { PDFViewer } from "pdfjs-dist/web/pdf_viewer";
import "pdfjs-dist/web/pdf_viewer.css";
pdfjsLib.GlobalWorkerOptions.workerSrc = "https://cdn.jsdelivr.net/npm/pdfjs-dist@2.0.943/build/pdf.worker.min.js";

export default({
  name: 'Tab1Page',
  components: { IonContent, IonPage },

  data(){
    return{
      url : 'https://firebasestorage.googleapis.com/v0/b/cynohub-v3.appspot.com/o/PDFUniversityNotes%2FFirst%20Year%2FJNTUH%2FEngineering%20Physics%2FOne%20Engineering%20Physics.pdf?alt=media&token=3b59970c-89b7-4edb-a51c-113d15d62627',
      number_of_pages_to_show : 5,
      scale : 0.5
    }
  },

  async mounted(){

      let container = document.getElementById("pageContainer");


      this.pdfViewer = new PDFViewer({
        container: container
      });


      let loadingTask = pdfjsLib.getDocument(this.url);

      let pdf = await loadingTask.promise;


      this.pdfViewer.setDocument(pdf, this.number_of_pages_to_show);


      this.pdfViewer._setScale(this.scale)


  }
});
</script>
