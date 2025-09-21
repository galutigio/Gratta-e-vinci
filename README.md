# Gratta-e-vinci
<!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8" />
<title>Gratta e Vinci Virtuale</title>
<style>
  .grid {
    display: grid;
    grid-template-columns: repeat(3, 120px);
    grid-gap: 10px;
    margin-bottom: 10px;
  }
  .cell {
    width: 120px;
    height: 80px;
    border: 2px solid #333;
    text-align: center;
    line-height: 80px;
    font-size: 18px;
    cursor: pointer;
    user-select: none;
    background-color: #ddd;
  }
  .revealed {
    background-color: #fff;
    cursor: default;
  }
  #restartBtn {
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
  }
</style>
</head>
<body>

<h2>Gratta e Vinci Virtuale</h2>
<p>Clicca sulle caselle per scoprire cosa c’è sotto!</p>
<div class="grid" id="grid"></div>
<p id="message"></p>
<button id="restartBtn">Ricomincia</button>

<script>
  const boxesOriginal = [
    { type: 'win', label: 'Valigia' },
    { type: 'win', label: 'Hotel' },
    { type: 'penalty', label: 'Cantare una canzone' },
    { type: 'penalty', label: 'Raccontare una barzelletta' },
    { type: 'penalty', label: 'Fare 10 saltelli' },
    { type: 'penalty', label: 'Bere un bicchiere d’acqua' },
    { type: 'penalty', label: 'Dire un complimento a qualcuno' },
    { type: 'penalty', label: 'Fare un giro su te stesso' },
    { type: 'penalty', label: 'Fare una faccia buffa' }
  ];

  let boxes = [];

  const grid = document.getElementById('grid');
  const message = document.getElementById('message');
  const restartBtn = document.getElementById('restartBtn');

  function shuffle(array) {
    for (let i = array.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [array[i], array[j]] = [array[j], array[i]];
    }
  }

  function createGrid() {
    grid.innerHTML = '';
    message.textContent = '';
    boxes = [...boxesOriginal];
    shuffle(boxes);

    boxes.forEach((box, index) => {
      const cell = document.createElement('div');
      cell.className = 'cell';
      cell.addEventListener('click', () => {
        if (cell.classList.contains('revealed')) return;

        cell.classList.add('revealed');
        cell.textContent = box.label;

        if (box.type === 'win') {
          message.textContent = `Complimenti! Hai trovato il simbolo vincente: ${box.label}`;
        } else {
          message.textContent = `Penitenza: ${box.label}`;
        }
      });
      grid.appendChild(cell);
    });
  }

  restartBtn.addEventListener('click', () => {
    createGrid();
  });

  // Inizializza al caricamento
  createGrid();
</script>

</body>
</html>
