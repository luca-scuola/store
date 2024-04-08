<script>
  import { onMount } from 'svelte';
  import Chart from 'chart.js/auto';


  let canvasElement;

  // Uso l'hook onMount per caricare i dati non appena il componente viene montato.
  onMount(async () => {
    const response = await fetch('../shopping_trends_updated.csv');
    if (response.ok) {
      const csvText = await response.text();
      const items = parseCSV(csvText);
      const ageData = prepareAgeData(items);
      updateBarChart(ageData);
    } else {
      console.error('Failed to fetch data:', response.status);
    }
  });

  function parseCSV(csvText) {
    // Divido il CSV in righe.
    const lines = csvText.split('\n');
    // La prima riga contiene gli header, quindi va separata dal resto.
    const headers = lines.shift().split(',');
    
    // Per ogni riga, creo un oggetto dove ogni header diventa una chiave.
    return lines.map(line => {
      const values = line.split(',');
      return headers.reduce((object, header, index) => {
        object[header] = values[index];
        return object;
      }, {});
    });
  }

  function prepareAgeData(items) {
    const ageCounts = items.reduce((acc, item) => {
      const age = item.Age;
      if (age) {
        acc[age] = (acc[age] || 0) + 1;
      }
      return acc;
    }, {});

    // Restituisco un oggetto con le etichette (età) e i dati (conteggi) per il grafico.
    return {
      labels: Object.keys(ageCounts),
      data: Object.values(ageCounts),
    };
  }

  function updateBarChart(ageData) {
    const data = {
      labels: ageData.labels,
      datasets: [{
        label: 'Numero di Compratori per età',
        data: ageData.data,
        backgroundColor: 'rgba(54, 162, 235, 0.5)',
        borderColor: 'rgba(54, 162, 235, 1)',
        borderWidth: 1,
      }]
    };


       const config = {
     type: 'bar',
     data: data,
     options: {
       responsive: true,
       maintainAspectRatio: false,
       animation: {
         duration: 800, 
       },
       scales: {
         x: {
           title: {
             display: true,
             text: 'Età'
           }
         },
         y: {
           title: {
             display: true,
             text: 'Numero di Compratori'
           }
         }
       }
     }
   };
   new Chart(canvasElement, config);
 }
</script>
<style> 
div { 
  margin-top: 20px; 
} 
canvas { 
  max-width: 100%; 
  height: 500px; 
  margin: auto;
}
  
</style>
<div>
<canvas bind:this={canvasElement}></canvas>
</div>