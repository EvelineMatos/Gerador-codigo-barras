# Gerador-codigo-barras


# README - fnGeradorBoletos

## 📌 Visão Geral

Este projeto é uma Azure Function que gera códigos de barras para boletos bancários e envia os resultados para uma fila do Azure Service Bus. A função expõe um endpoint HTTP que recebe os dados do boleto (valor e data de vencimento) e retorna o código de barras gerado junto com uma imagem PNG em formato base64.

## 🚀 Funcionalidades

- Geração de código de barras no padrão bancário (44 caracteres)
- Validação dos dados de entrada (valor e data de vencimento)
- Criação de imagem do código de barras em formato PNG
- Conversão da imagem para base64
- Integração com Azure Service Bus para envio dos resultados
- Endpoint HTTP protegido com AuthorizationLevel.Function

## 🛠️ Pré-requisitos

- .NET 8.0 SDK
- Azure Functions Core Tools
- Conta Azure com acesso ao Service Bus
- Visual Studio ou VS Code (recomendado)

## 🔧 Configuração

1. Clone o repositório:
   ```bash
   git clone [URL_DO_REPOSITORIO]
   cd fnGeradorBoletos
   ```

2. Configure as variáveis de ambiente no arquivo `local.settings.json`:
   ```json
   {
     "IsEncrypted": false,
     "Values": {
       "AzureWebJobsStorage": "UseDevelopmentStorage=true",
       "FUNCTIONS_WORKER_RUNTIME": "dotnet",
       "ServiceBusConnectionString": "[SUA_STRING_DE_CONEXAO_DO_SERVICE_BUS]"
     }
   }
   ```

3. Instale as dependências:
   ```bash
   dotnet restore
   ```

## 🏃 Executando Localmente

1. Inicie o Azure Storage Emulator (ou use uma conta real)
2. Execute a função:
   ```bash
   func start
   ```

3. A função estará disponível em:
   ```
   http://localhost:7071/api/barcode-generate
   ```

## 📡 Chamando a API

Envie uma requisição POST para o endpoint com o seguinte corpo:

```json
{
  "valor": "100.50",
  "dataVencimento": "2025-12-31"
}
```

Exemplo usando cURL:
```bash
curl -X POST "http://localhost:7071/api/barcode-generate" \
-H "Content-Type: application/json" \
-d '{"valor": "100.50", "dataVencimento": "2025-12-31"}'
```

## 📦 Estrutura do Projeto

```
fnGeradorBoletos/
├── Function1.cs            # Código principal da função
├── host.json               # Configurações do host do Azure Functions
├── local.settings.json     # Configurações locais (não versionado)
├── fnGeradorBoletos.csproj # Configurações do projeto e dependências
└── .gitignore             # Arquivos ignorados pelo Git
```

## ⚙️ Dependências

- Azure.Messaging.ServiceBus (7.18.4)
- BarcodeLib (3.1.5)
- Microsoft.Azure.Functions.Worker (2.0.0)
- Newtonsoft.Json (13.0.3)

## 🚀 Implantação no Azure

1. Crie um Function App no Azure Portal
2. Configure a string de conexão do Service Bus nas configurações da aplicação
3. Implante o projeto usando:
   ```bash
   func azure functionapp publish [NOME_DO_FUNCTION_APP]
   ```

## 📄 Licença

Este projeto está sob a licença MIT. Consulte o arquivo LICENSE para mais detalhes.

## 🤝 Contribuições

Contribuições são bem-vindas! Por favor, abra uma issue ou envie um pull request.