<div class="home-container">
  <h1>Benvenuto nel Nostro Progetto di Analisi Dati!</h1>
  <p>Esplora le tendenze di acquisto attraverso analisi dettagliate e interattive.</p>

  <div class="overview">
    <div class="card">
      <h2>Analisi Genere</h2>
      <p>Scopri la distribuzione di genere tra i compratori.</p>
      <a href="/sesso">Esplora Genere</a>
    </div>
    <div class="card">
      <h2>Analisi Età</h2>
      <p>Visualizza le tendenze di acquisto per fascia d'età.</p>
      <a href="/eta">Esplora Età</a>
    </div>
    <div class="card">
      <h2>Analisi Oggetti</h2>
      <p>Visualizza le tendenze di acquisto per fascia di prezzo e per categoria.</p>
      <a href="/oggetti">Esplora Oggetti</a>
    </div>

  </div>

</div>

<style>
  .home-container {
    text-align: center;
    padding: 40px;

  }

  .home-container p {
    margin-bottom: 40px; 
  }

  .overview {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    gap: 20px;
    margin-top: 40px; 
  }

  .card {
    padding: 20px;
    border: none; 
    border-radius: 10px; 
    width: calc(30% - 20px); 
    box-shadow: 0 4px 6px rgba(0,0,0,0.1); 
    transition: transform 0.3s ease, box-shadow 0.3s ease; 
    background-color: #ffffff; 
  }

  .card:hover {
    transform: translateY(-5px); 
    box-shadow: 0 10px 15px rgba(0,0,0,0.2); 
  }

  a {
    background-color: #007bff;
    color: white;
    padding: 12px 24px;
    margin: 20px 0; 
    border-radius: 5px;
    text-decoration: none;
    transition: background-color 0.3s ease;
  }

  a:hover {
    background-color: #0056b3;
  }
</style>




