<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Chatbot de Rifa</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f2f2f2;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .chatbot-container {
      width: 360px;
      background: #fff;
      border-radius: 10px;
      box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
      overflow: hidden;
    }

    .chat-header {
      background: #0d6efd;
      color: #fff;
      padding: 15px;
      font-size: 18px;
      font-weight: bold;
      text-align: center;
    }

    .chatbox {
      padding: 15px;
      max-height: 70vh;
      overflow-y: auto;
    }

    .bot-message {
      background: #e9ecef;
      padding: 10px 15px;
      border-radius: 8px;
      margin-bottom: 10px;
    }

    .bot-options button {
      margin: 5px 5px 0 0;
      padding: 10px;
      border: none;
      background: #0d6efd;
      color: #fff;
      border-radius: 5px;
      cursor: pointer;
    }

    .bot-options button:hover {
      background: #0b5ed7;
    }

    a {
      color: #0d6efd;
      text-decoration: none;
    }
  </style>
</head>
<body>
  <div class="chatbot-container">
    <div class="chat-header">🎟️ RifaBot</div>
    <div class="chatbox" id="chatbox">
      <div class="bot-message">Olá! 👋 Bem-vindo(a) à <strong>Rifa Premiada</strong>! Como posso ajudar?</div>
      <div class="bot-options">
        <button onclick="handleOption('rifas')">🎟️ Ver Rifas</button>
        <button onclick="handleOption('contato')">🛠️ Falar com a Equipe</button>
        <button onclick="handleOption('faq')">❓ Dúvidas Frequentes</button>
      </div>
    </div>
  </div>

  <script>
    function handleOption(option) {
      const chatbox = document.getElementById("chatbox");

      let response = "";
      if (option === "rifas") {
        response = `
          <div class="bot-message">
            📌 <strong>Rifas Disponíveis:</strong><br><br>
            🔹 <b>iPhone 15 Pro</b><br>
            Valor: R$2,00 por número<br>
            Sorteio: 20/08/2025<br>
            👉 <a href="#">Participar</a><br><br>

            🔹 <b>Pix de R$1.000</b><br>
            Valor: R$2,00 por número<br>
            Sorteio: 15/08/2025<br>
            👉 <a href="#">Participar</a>
          </div>
        `;
      } else if (option === "contato") {
        response = `
          <div class="bot-message">
            🤝 Fale com nossa equipe:<br><br>
            📞 WhatsApp: <a href="https://wa.me/5599999999999" target="_blank">Clique aqui</a><br>
            📧 Email: suporte@rifapremiada.com<br>
            ⏰ Atendimento: Seg a Sex, das 9h às 18h
          </div>
        `;
      } else if (option === "faq") {
        response = `
          <div class="bot-message">
            ❓ <strong>Dúvidas Frequentes</strong><br><br>
            <b>Como funciona a rifa?</b><br>
            Você escolhe o número, paga via Pix e participa do sorteio.<br><br>

            <b>Como recebo o prêmio?</b><br>
            Entramos em contato pelo WhatsApp ou e-mail após o sorteio.<br><br>

            <b>Posso comprar quantos números?</b><br>
            Quantos quiser, enquanto houver disponibilidade.
          </div>
        `;
      }

      chatbox.innerHTML += response;
      chatbox.scrollTop = chatbox.scrollHeight;
    }
  </script>
</body>
</html>
