<script>
  import { onMount } from 'svelte';
  import Chart from 'chart.js/auto';

  let canvasElement;
  let totalBuyers = 0;
  let maschiPercentage = 0;
  let femminePercentage = 0;

onMount(() => {
  fetch('../shopping_trends_updated.csv')
    .then(response => {
      if (response.ok) {
        return response.text();
      } else {
        throw new Error('Failed to fetch data: ' + response.status);
      }
    })
    .then(csvText => {
      const items = parseCSV(csvText);
      const genderCounts = countGenders(items);

      // Calcola totali e percentuali dopo aver ottenuto genderCounts
      totalBuyers = Object.values(genderCounts).reduce((acc, curr) => acc + curr, 0);
      maschiPercentage = ((genderCounts.Maschi / totalBuyers) * 100).toFixed(2);
      femminePercentage = ((genderCounts.Femmine / totalBuyers) * 100).toFixed(2);

      updateChart(genderCounts);
    })
    .catch(error => {
      console.error(error.message);
    });
});


  function parseCSV(csvText) {
    const lines = csvText.split('\n');
    const headers = lines.shift().split(',');
    return lines.map(line => {
      const values = line.split(',');
      return headers.reduce((object, header, index) => {
        object[header] = values[index];
        return object;
      }, {});
    });
  }

  function countGenders(items) {
    return items.reduce((acc, item) => {
        const gender = item.Gender;
        if (gender === 'Male' || gender === 'Female') { 
            const genderKey = gender === 'Male' ? 'Maschi' : 'Femmine'; 
            acc[genderKey] = (acc[genderKey] || 0) + 1;
        }
        return acc;
    }, {});
  }

  function updateChart(genderCounts) {
    const data = {
      datasets: [{
        data: Object.values(genderCounts),
        backgroundColor: ['blue', '#FF407B'],
      }],
      labels: ['Maschi', 'Femmine'],
    };

    const config = {
      type: 'pie',
      data: data,
      options: {
        responsive: true,
        maintainAspectRatio: true,
        plugins: {
          legend: {
            onClick: (e) => e.stopPropagation()
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
    max-width: 400px;
    max-height: 400px;
    margin: auto;
  }

  .insights {
    text-align: center;
    margin-top: 40px;
  }
</style>

<div>
  <canvas bind:this={canvasElement}></canvas>
  <div class="insights">
    <h2>Approfondimenti</h2>
    <p>Numero totale di compratori analizzati: {totalBuyers}</p>
    <p>Percentuale di Maschi: {maschiPercentage}%</p>
    <p>Percentuale di Femmine: {femminePercentage}%</p>
  </div>
</div>
