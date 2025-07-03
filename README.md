<!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8" />
<title>Giochino Estivo - Estrazione Regali</title>
<style>
  body {
    font-family: 'Comic Sans MS', cursive, sans-serif;
    background: linear-gradient(to bottom, #87ceeb 0%, #fefbd8 100%);
    text-align: center;
    padding: 20px;
  }
  h1 {
    color: #ff4500;
    margin-bottom: 30px;
  }
  .container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 20px;
  }
  .card {
    background: white;
    border-radius: 15px;
    box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    width: 140px;
    padding: 15px;
    cursor: pointer;
    transition: transform 0.2s ease;
  }
  .card:hover {
    transform: scale(1.1);
    box-shadow: 0 6px 15px rgba(255,69,0,0.5);
  }
  .emoji {
    font-size: 60px;
    margin-bottom: 10px;
  }
  .regalo {
    font-weight: bold;
    color: #007acc;
    min-height: 40px;
    margin-top: 10px;
    font-size: 14px;
    visibility: hidden; /* regalo nascosto finché non clicchi */
  }
  #risultato {
    margin-top: 30px;
    font-size: 24px;
    color: #ff4500;
    font-weight: bold;
    min-height: 40px;
  }
  #btnRimescola {
    margin-top: 20px;
    font-size: 18px;
    padding: 10px 25px;
    background: #ff4500;
    color: white;
    border: none;
    border-radius: 10px;
    cursor: pointer;
  }
  #btnRimescola:hover {
    background: #e03e00;
  }
</style>
</head>
<body>

<h1>☀️ Giulia Summer's Vibes ☀️</h1>

<div class="container" id="containerOggetti">
  <!-- Oggetti con emoji come segnaposto -->
</div>

<button id="btnRimescola">Rimescola i regali 🔄</button>

<div id="risultato"></div>

<script>
  const oggetti = [
    {nome: 'Ombrellone', emoji: '⛱️'},
    {nome: 'Secchiello', emoji: '🪣'},
    {nome: 'Salvagente', emoji: '🛟'},
    {nome: 'Palma', emoji: '🌴'},
    {nome: 'Sole', emoji: '☀️'},
    {nome: 'Mare', emoji: '🌊'},
    {nome: 'Pina Colada', emoji: '🍹'},
    {nome: 'Tavola Surf', emoji: '🏄‍♂️'},
    {nome: 'Maschera da Sub', emoji: '🤿'}
  ];

  const regali = [
    "Foto sexy",
    "Foto culo",
    "Foto topless",
    "Video sexy",
    "Video hot",
    "Sconto 50%",
    "Sconto 20%",
    "Sorpresa in chat",
    "Audio Sexy"
  ];

  let regaliAssegnati = [];

  const container = document.getElementById('containerOggetti');
  const risultato = document.getElementById('risultato');
  const btnRimescola = document.getElementById('btnRimescola');

  function shuffle(array) {
    for (let i = array.length -1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i+1));
      [array[i], array[j]] = [array[j], array[i]];
    }
  }

  function creaCards() {
    container.innerHTML = '';
    oggetti.forEach((oggetto, i) => {
      const card = document.createElement('div');
      card.className = 'card';
      card.dataset.index = i;

      const emojiDiv = document.createElement('div');
      emojiDiv.className = 'emoji';
      emojiDiv.textContent = oggetto.emoji;
      card.appendChild(emojiDiv);

      const nomeDiv = document.createElement('div');
      nomeDiv.textContent = oggetto.nome;
      card.appendChild(nomeDiv);

      const regaloDiv = document.createElement('div');
      regaloDiv.className = 'regalo';
      regaloDiv.textContent = '';
      card.appendChild(regaloDiv);

      card.onclick = () => {
        const regalo = regaliAssegnati[i];
        regaloDiv.textContent = regalo;
        regaloDiv.style.visibility = 'visible';
        risultato.textContent = `Hai scelto: ${oggetto.nome} → 🎁 ${regalo}!`;
      };

      container.appendChild(card);
    });
  }

  function assegnaRegali() {
    regaliAssegnati = [...regali];
    shuffle(regaliAssegnati);

    const cards = container.querySelectorAll('.card');
    cards.forEach(card => {
      const regaloDiv = card.querySelector('.regalo');
      regaloDiv.textContent = '';
      regaloDiv.style.visibility = 'hidden';
    });

    risultato.textContent = '🎲 Regali rimescolati! Scegli un oggetto per scoprire il regalo.';
  }

  creaCards();
  assegnaRegali();

  btnRimescola.onclick = () => {
    assegnaRegali();
  };
</script>

</body>
</html>
