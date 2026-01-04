---
layout: cv
title: CV
---

<div id="pdf-viewer"></div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
<script>
  pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';
  
  const pdfUrl = '{{ "/assets/files/ResumeNelcifran.pdf" | relative_url }}';
  
  pdfjsLib.getDocument(pdfUrl).promise.then(pdf => {
    const container = document.getElementById('pdf-viewer');
    
    for (let pageNum = 1; pageNum <= pdf.numPages; pageNum++) {
      pdf.getPage(pageNum).then(page => {
        const canvas = document.createElement('canvas');
        const ctx = canvas.getContext('2d');
        const viewport = page.getViewport({scale: 1.5});
        canvas.width = viewport.width;
        canvas.height = viewport.height;
        canvas.style.marginBottom = '20px';
        canvas.style.border = '1px solid #ddd';
        
        page.render({canvasContext: ctx, viewport: viewport});
        container.appendChild(canvas);
      });
    }
  });
</script>
