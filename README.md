index.html

<!DOCTYPE html>More actions
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Escalação do Time</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header>
    <h1>Escalação
    </h1>
    <button id="toggle-theme">Alternar Tema</button>
  </header>

  <main>
    <section id="escalar-jogador">
      <h2>Escalar Jogador</h2>
      <form id="form-escalar">
        <input type="text" id="posicao" placeholder="Posição" required>
        <input type="text" id="nome" placeholder="Nome" required>
        <input type="number" id="numero" placeholder="Número" required>
        <button type="submit">Escalar</button>
      </form>
    </section>

    <section id="remover-jogador">
      <h2>Remover Jogador</h2>
      <form id="form-remover">
        <input type="number" id="numero-remover" placeholder="Número do jogador" required>
        <button type="submit">Remover</button>
      </form>
    </section>

    <section id="lista-time">
      <h2>Lista do Time</h2>
      <ul id="time-lista"></ul>
    </section>
  </main>

  <script src="script.js"></script>
</body>
</html>



script.js

document.addEventListener("DOMContentLoaded", () => {More actions
    const formEscalar = document.getElementById("form-escalar");
    const formRemover = document.getElementById("form-remover");
    const listaTime = document.getElementById("time-lista");
    const toggleThemeButton = document.getElementById("toggle-theme");
    const body = document.body;
  
    formEscalar.addEventListener("submit", (event) => {
      event.preventDefault();
      const posicao = document.getElementById("posicao").value.trim();
      const nome = document.getElementById("nome").value.trim();
      const numero = document.getElementById("numero").value.trim();
  
      if (posicao && nome && numero) {
        if (confirm(`Deseja escalar o jogador ${nome} (Nº ${numero}) na posição ${posicao}?`)) {
          const li = document.createElement("li");
          li.textContent = `${posicao}: ${nome} (Nº ${numero})`;
          li.setAttribute("data-numero", numero);
          listaTime.appendChild(li);
  
          formEscalar.reset();
        }
      } else {
        alert("Todos os campos devem ser preenchidos!");
      }
    });
  
    formRemover.addEventListener("submit", (event) => {
      event.preventDefault();
      const numeroRemover = document.getElementById("numero-remover").value.trim();
  
      if (numeroRemover) {
        const jogador = listaTime.querySelector(`li[data-numero="${numeroRemover}"]`);
        if (jogador) {
          if (confirm(`Deseja remover o jogador Nº ${numeroRemover}?`)) {
            jogador.remove();
            formRemover.reset();
          }
        } else {
          alert("Jogador não encontrado!");
        }
      } else {
        alert("O número do jogador deve ser preenchido!");
      }
    });
  
    toggleThemeButton.addEventListener("click", () => {
      body.classList.toggle("dark-theme");
    });
  });

  style.css

  body {More actions
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f4f4f4;
    color: #333;
  }
  
  header {
    background-color: #0cbddc;
    color: white;
    padding: 1rem;
    text-align: center;
  }
  
  header button {
    margin-top: 10px;
    padding: 0.5rem;
    border: none;
    background: white;
    color: #0e7dcc;
    cursor: pointer;
    border-radius: 5px;
  }
  
  main {
    max-width: 800px;
    margin: 2rem auto;
    padding: 1rem;
    background: white;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }
  
  section {
    margin-bottom: 2rem;
  }
  
  h2 {
    color: #000000;
  }
  
  form input, form button {
    margin: 0.5rem 0;
    padding: 0.5rem;
    width: calc(100% - 1rem);
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  
  form button {
    background-color: #6db5f8;
    color: white;
    cursor: pointer;
  }
  
  form button:hover {
    background-color: #0092ed;
  }
  
  #time-lista {
    list-style-type: none;
    padding: 0;
  }
  
  #time-lista li {
    margin: 0.5rem 0;
    padding: 0.5rem;
    background-color: #f9f9f9;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  
  .dark-theme {
    background-color: #333;
    color: white;
  }
  
  .dark-theme header {
    background-color: #222;
    color: #ddd;
  }
  
  .dark-theme main {
    background: #d2c7c7;
    color: white;
  }
