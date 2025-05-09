

<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ternos Sob Medida - Mauricio Castello</title>
  <link rel="manifest" href="data:application/manifest+json;base64,eyJuYW1lIjogIlRlcm5vcyBTb2IgTWVkaWRhIiwgInNob3J0X25hbWUiOiAiVGVybm9zTWVkIiwgImljb25zIjogW3sic3JjIjogImljb24ucG5nIiwgInNpemVzIjogIjMyeDMyIn1dLCAiYmFja2dyb3VuZCI6ICIjMmM1MzY0IiwgInRoZW1lX2NvbG9yIjogIiMwZjIwMjciLCAic3RhcnRfdXJsIjogIi8ifQ==" />
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background: #f4f4f4;
      color: #333;
    }
    header, footer {
      background: #2c5364;
      color: white;
      padding: 20px;
      text-align: center;
    }
    .container {
      padding: 20px;
    }
    .step {
      display: none;
    }
    .step.active {
      display: block;
    }
    .options img {
      width: 100px;
      margin: 10px;
      border: 2px solid transparent;
      cursor: pointer;
    }
    .options img.selected {
      border-color: #2c5364;
    }
    input, select, button {
      padding: 10px;
      margin: 5px 0;
      width: 100%;
      box-sizing: border-box;
    }
    button {
      background-color: #2c5364;
      color: white;
      border: none;
      cursor: pointer;
    }
    button:hover {
      background-color: #203a43;
    }
  </style>
</head>
<body>
  <header>
    <h1>Ternos Sob Medida</h1>
    <p>Alfaiataria por Mauricio Castello</p>
  </header>
  <div class="container">
    <div id="step1" class="step active">
      <h2>1. Escolha o Modelo</h2>
      <div class="options" id="modelos">
        <img src="https://via.placeholder.com/100x120?text=Modelo+1" data-modelo="Modelo 1" />
        <img src="https://via.placeholder.com/100x120?text=Modelo+2" data-modelo="Modelo 2" />
        <img src="https://via.placeholder.com/100x120?text=Modelo+3" data-modelo="Modelo 3" />
      </div>
      <button onclick="proximoPasso(2)">Próximo</button>
    </div>
    <div id="step2" class="step">
      <h2>2. Insira suas Medidas</h2>
      <input type="text" id="altura" placeholder="Altura (cm)" />
      <input type="text" id="ombro" placeholder="Largura do Ombro (cm)" />
      <input type="text" id="peito" placeholder="Circunferência do Peito (cm)" />
      <input type="text" id="cintura" placeholder="Cintura (cm)" />
      <input type="text" id="quadril" placeholder="Quadril (cm)" />
      <button onclick="proximoPasso(3)">Próximo</button>
    </div>
    <div id="step3" class="step">
      <h2>3. Escolha a Cor</h2>
      <select id="cor">
        <option>Preto</option>
        <option>Azul Marinho</option>
        <option>Cinza</option>
        <option>Vinho</option>
      </select>
      <button onclick="proximoPasso(4)">Próximo</button>
    </div>
    <div id="step4" class="step">
      <h2>4. Resumo do Pedido</h2>
      <p><strong>Modelo:</strong> <span id="resumoModelo"></span></p>
      <p><strong>Altura:</strong> <span id="resumoAltura"></span> cm</p>
      <p><strong>Ombro:</strong> <span id="resumoOmbro"></span> cm</p>
      <p><strong>Peito:</strong> <span id="resumoPeito"></span> cm</p>
      <p><strong>Cintura:</strong> <span id="resumoCintura"></span> cm</p>
      <p><strong>Quadril:</strong> <span id="resumoQuadril"></span> cm</p>
      <p><strong>Cor:</strong> <span id="resumoCor"></span></p>
      <h3>Finalizar Pedido</h3>
      <button onclick="enviarWhatsapp()">Enviar via WhatsApp</button>
      <button onclick="enviarEmail()">Enviar por E-mail</button>
      <button onclick="pagarPix()">Pagar via Pix</button>
      <button onclick="pagarMercadoPago()">Pagar com Mercado Pago</button>
    </div>
  </div>
  <footer>
    <p>© 2025 Mauricio Castello - Alfaiataria sob medida</p>
  </footer>
  <script>
    let modeloSelecionado = "";
    document.querySelectorAll("#modelos img").forEach(img => {
      img.onclick = () => {
        document.querySelectorAll("#modelos img").forEach(i => i.classList.remove("selected"));
        img.classList.add("selected");
        modeloSelecionado = img.dataset.modelo;
      };
    });

    function proximoPasso(n) {
      if (n === 2 && !modeloSelecionado) {
        alert("Escolha um modelo primeiro.");
        return;
      }
      document.querySelectorAll(".step").forEach(s => s.classList.remove("active"));
      document.getElementById("step" + n).classList.add("active");
      if (n === 4) preencherResumo();
    }

    function preencherResumo() {
      document.getElementById("resumoModelo").textContent = modeloSelecionado;
      document.getElementById("resumoAltura").textContent = document.getElementById("altura").value;
      document.getElementById("resumoOmbro").textContent = document.getElementById("ombro").value;
      document.getElementById("resumoPeito").textContent = document.getElementById("peito").value;
      document.getElementById("resumoCintura").textContent = document.getElementById("cintura").value;
      document.getElementById("resumoQuadril").textContent = document.getElementById("quadril").value;
      document.getElementById("resumoCor").textContent = document.getElementById("cor").value;
    }

    function enviarWhatsapp() {
      const msg = gerarMensagemPedido();
      window.open(`https://wa.me/5546991081445?text=${encodeURIComponent(msg)}`);
    }

    function enviarEmail() {
      const assunto = "Pedido de Terno Sob Medida";
      const corpo = gerarMensagemPedido();
      window.location.href = `mailto:mauriciocastello30@gmail.com?subject=${encodeURIComponent(assunto)}&body=${encodeURIComponent(corpo)}`;
    }

    function pagarPix() {
      alert("Chave Pix: 46991081445");
    }

    function pagarMercadoPago() {
      window.open("https://www.mercadopago.com.br", "_blank");
    }

    function gerarMensagemPedido() {
      return `Pedido de Terno Sob Medida:
Modelo: ${modeloSelecionado}
Altura: ${document.getElementById("altura").value} cm
Ombro: ${document.getElementById("ombro").value} cm
Peito: ${document.getElementById("peito").value} cm
Cintura: ${document.getElementById("cintura").value} cm
Quadril: ${document.getElementById("quadril").value} cm
Cor: ${document.getElementById("cor").value}`;
    }

    if ('serviceWorker' in navigator) {
      navigator.serviceWorker.register('data:text/javascript;base64,Ci8vIFNlcnZpY2UgV29ya2VyIFNpbXBsZXMKc2VsZi5hZGRFdmVudExpc3RlbmVyKCdpbnN0YWxsJywgZXZlbnQgPT4gewogIGV2ZW50LndhaXQoKTsKICBzZWxmLnNraXdoYWl0V2FpdCgpOwp9KTsKCnNlbGYuYWRkRXZlbnRMaXN0ZW5lcignZmV0Y2gnLCBldmVudCA9PiB7CiAgZXZlbnQucmVzcG9uZFdpdGgoCiAgICB7CiAgICAgIHJlc3BvbnNlOiAnY2FjaGUnCiAgICB9CiAgKTsKfSk7', { type: 'module' });
    }
  </script>
</body>
</html>
