<!DOCTYPE html>
<html>
<head>
    <title>Envio de Mensagens no WhatsApp</title>
    <style>
        body {
            background-color: #000;
            color: #fff;
            font-family: Arial, sans-serif;
        }

        h1, h2 {
            color: #ff0000;
        }

        label {
            display: block;
            margin-top: 10px;
            font-size: 16px;
        }

        input[type="file"] {
            margin-top: 5px;
        }

        textarea {
            width: 300px;
            height: 100px;
            resize: none;
            margin-top: 10px;
        }

        button[type="submit"] {
            background-color: #ff0000;
            color: #fff;
            padding: 10px 20px;
            border: none;
            cursor: pointer;
            font-size: 16px;
            margin-top: 10px;
        }

        button[type="submit"]:hover {
            background-color: #ff3333;
        }

        .whatsapp-button {
            background-color: #25D366;
            color: #fff;
            padding: 10px 20px;
            border: none;
            cursor: pointer;
            font-size: 16px;
            margin-top: 10px;
            text-decoration: none;
            display: inline-block;
        }

        .whatsapp-button:hover {
            background-color: #128C7E;
        }
    </style>
</head>
<body>
    <h1>Envio de Mensagens no WhatsApp</h1>
    <form action="/enviar" method="post" enctype="multipart/form-data">
        <label for="arquivo">Selecione o arquivo CSV:</label>
        <input type="file" id="arquivo" name="arquivo" accept=".csv">

        <label for="mensagem">Mensagem Personalizada:</label>
        <textarea id="mensagem" name="mensagem" placeholder="Digite sua mensagem personalizada..."></textarea>

        <label for="anexo">Anexar arquivo:</label>
        <input type="file" id="anexo" name="anexo" accept=".jpg, .jpeg, .png, .gif, .mp4, .pdf, .doc, .docx">

        <button type="submit">Enviar Mensagens</button>
    </form>

    <h2>Números de Telefone:</h2>
    <div id="botoes"></div>

    <h2>Conectar ao WhatsApp Web:</h2>
    <a href="https://web.whatsapp.com/" target="_blank" class="whatsapp-button">Conectar ao WhatsApp Web</a>

    <script>
        // Função para criar botões com números de telefone
        function criarBotao(numero) {
            var botao = document.createElement('button');
            botao.innerHTML = numero;
            botao.name = 'telefones';
            botao.value = numero;
            document.getElementById('botoes').appendChild(botao);
        }

        // Função para ler o arquivo CSV selecionado
        function lerArquivo(event) {
            var input = event.target;
            var reader = new FileReader();

            reader.onload = function(){
                var linhas = reader.result.split('\n');
                for (var i = 1; i < linhas.length; i++) {
                    var numero = linhas[i].split(',')[0].trim();
                    criarBotao(numero);
                }
            };

            reader.readAsText(input.files[0]);
        }

        // Evento de alteração do arquivo selecionado
        document.getElementById('arquivo').addEventListener('change', lerArquivo);
    </script>
</body>
</html>
