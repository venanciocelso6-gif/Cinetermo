// 🎯 CINETERMO — Jogo tipo "Termo" com tema de Cinética Química

const palavras = [
  "CALOR", "FATOR", "REAGE", "MOLAR", "ATOMO",
  "MASSA", "GASES", "ACIDO", "BASES", "TEMPO", "DILUI", "FUSAO", "VAPOR", "LENTO", "CATAL".
];

let palavraSecreta = palavras[Math.floor(Math.random() * palavras.length)];
let tentativas = 0;
const maxTentativas = 6;

// Cria o tabuleiro
const board = document.getElementById("board");
for (let i = 0; i < maxTentativas * 5; i++) {
  const tile = document.createElement("div");
  tile.classList.add("tile");
  board.appendChild(tile);
}

// Função principal — checa o palpite
function checkGuess() {
  const input = document.getElementById("guess");
  const tentativa = input.value.toUpperCase();

  if (tentativa.length !== 5) {
    alert("Digite uma palavra com 5 letras!");
    return;
  }

  const start = tentativas * 5;
  for (let i = 0; i < 5; i++) {
    const tile = board.children[start + i];
    tile.textContent = tentativa[i];

    if (tentativa[i] === palavraSecreta[i]) {
      tile.classList.add("correct");
    } else if (palavraSecreta.includes(tentativa[i])) {
      tile.classList.add("present");
    } else {
      tile.classList.add("absent");
    }
  }

  tentativas++;
  input.value = "";

  if (tentativa === palavraSecreta) {
    document.getElementById("message").textContent =
      "🎉 Acertou! A palavra era " + palavraSecreta + "!";
    input.disabled = true;
  } else if (tentativas >= maxTentativas) {
    document.getElementById("message").textContent =
      "💀 Fim de jogo! A palavra era " + palavraSecreta + ".";
    input.disabled = true;
  }
}