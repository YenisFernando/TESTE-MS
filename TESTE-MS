<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Monitor de Conexão com Registro</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            background-color: #f2f2f2;
            margin: 0;
        }
        #status {
            padding: 10px;
            border-radius: 5px;
            text-align: center;
            font-size: 1.5em;
            margin-bottom: 20px;
        }
        .online {
            color: green;
            background-color: #e0ffe0;
        }
        .offline {
            color: red;
            background-color: #ffe0e0;
        }
        table {
            width: 80%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        th, td {
            border: 1px solid #ccc;
            padding: 10px;
            text-align: center;
        }
        th {
            background-color: #00796b;
            color: white;
        }
    </style>
</head>
<body>

<div id="status" class="offline">Verificando conexão...</div>

<table>
    <thead>
        <tr>
            <th>Data e Hora</th>
            <th>Latência (ms)</th>
            <th>Status</th>
        </tr>
    </thead>
    <tbody id="registro"></tbody>
</table>

<script>
    function verificarConexao() {
        const inicio = Date.now();
        let timeout = setTimeout(() => {
            adicionarRegistro(new Date().toLocaleString(), "-", "Perda de Conexão");
            document.getElementById("status").innerText = "Perda de conexão detectada";
            document.getElementById("status").className = "offline";
        }, 1000); // Marca perda de conexão após 1 segundo sem resposta

        fetch("https://www.google.com", { mode: "no-cors" })
            .then(() => {
                clearTimeout(timeout);
                const tempoResposta = Date.now() - inicio;
                document.getElementById("status").innerText = `Conectado (Latência: ${tempoResposta} ms)`;
                document.getElementById("status").className = "online";
                adicionarRegistro(new Date().toLocaleString(), `${tempoResposta} ms`, "Conectado");
            })
            .catch(() => {
                clearTimeout(timeout);
                adicionarRegistro(new Date().toLocaleString(), "-", "Perda de Conexão");
                document.getElementById("status").innerText = "Perda de conexão detectada";
                document.getElementById("status").className = "offline";
            });
    }

    function adicionarRegistro(dataHora, latencia, status) {
        const registro = document.getElementById("registro");
        const linha = document.createElement("tr");
        linha.innerHTML = `
            <td>${dataHora}</td>
            <td>${latencia}</td>
            <td>${status}</td>
        `;
        registro.insertBefore(linha, registro.firstChild); // Adiciona o novo registro no topo
    }

    // Verificar conexão a cada 1 segundo
    setInterval(verificarConexao, 1000);
</script>

</body>
</html>
