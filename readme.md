# Agente de IA – Atendimento de Marmitaria

## Descrição

Este projeto implementa um **agente de IA** para atendimento de um restaurante de marmitas, desenvolvido no **N8N**.  
O agente permite que um usuário converse por chat, faça pedidos personalizados e finalize a compra de forma automatizada.  
O fluxo registra os pedidos em **Postgres** e pode ser testado via webhook público.

---

![<alt-text>](https://github.com/rockiir/agente-restaurante/blob/main/chrome_hylmAE0qhC.png)

## Funcionalidades

1. **Apresentação do cardápio**
   
   - Lista de produtos disponíveis .
   
   - Permite ao cliente consultar o cardápio a qualquer momento.

2. **Pedidos personalizados**
   
   - Aceita alterações como: “trocar arroz por macarrão”, “sem salada”, “adicionar ovo”.
   
   - Sugere substituições caso algum item esteja indisponível.

3. **Gestão de cupons**
   
   - Permite aplicar cupons de desconto válidos.
   
   - Interação realizada via **agente de cupom**.

4. **Finalização do pedido**
   
   - Coleta **nome, telefone e e-mail** do cliente obrigatoriamente.
   
   - Gera um resumo final do pedido em JSON.
   
   - Calcula o valor total (fictício).
   
   - Pergunta forma de pagamento:
     
     - Cartão: pagamento realizado no caixa.
     
     - Pix: gera QR code (simulado).

5. **Registro do pedido**
   
   - Salva os dados do pedido no banco **Postgres** com as seguintes informações:
     
     - Nome do cliente
     
     - Itens escolhidos
     
     - Personalizações
     
     - Valor total
     
     - Status do pedido (confirmado)

---

## Tecnologias Utilizadas

- **N8N** – ferramenta principal de automação.

- **Postgres** – armazenamento dos pedidos e cupons.

- **OpenAI GPT-4.1-mini** – modelo de IA generativa para interpretação de pedidos e respostas.

- **DeepSeek** – modelo adicional de IA para suporte ao fluxo.

- **Webhook público** – para testes de chat.

- **LangChain Nodes** – memória e ferramentas de parsing de saída estruturada.

- Streamlit para tela

---

## Estrutura do Fluxo

| Node                      | Função                                                            |
| ------------------------- | ----------------------------------------------------------------- |
| `Webhook`                 | Recebe mensagens do usuário via POST.                             |
| `Agente de pedidos`       | Processa mensagens, apresenta cardápio, lida com personalizações. |
| `Simple Memory`           | Mantém contexto da conversa.                                      |
| `agente cupom`            | Aplica cupons de desconto de forma oculta.                        |
| `Agente finalizar pedido` | Confirma informações, calcula total, gera JSON final.             |
| `Postgres Tool`           | Salva ou atualiza pedidos e cupons no banco.                      |
| `Respond to Webhook`      | Retorna resposta do agente ao usuário.                            |

Fluxo completo disponível no N8N, com nodes conectados para garantir atendimento contínuo e consistente.

---

## Testes

Para testar o agente:

1. Enviar uma requisição POST para o webhook ou acesse pelo link https://restaurante.raquelmatos.site/

2. Estrutura da requisição:

`{   "message": "Quero ver o cardápio",   "session_id": "identificador_unico_sessao" }`

3. Interaja com o chat enviando mensagens como:
   
   - "Quero um prato com arroz e feijão"
   
   - "Adicionar ovo"
   
   - "Aplicar cupom"
   
   - "Finalizar pedido"

4. O agente retornará respostas em **Markdown** com o resumo do pedido, sugestões e confirmação final.

---

## Observações

- O foco do projeto é a **funcionalidade e inteligência do agente***

- O JSON final do pedido é **limpo e pronto para registro** no banco.

- Os cupons aplicados são fictícios e validados apenas internamente.

---

## Entregáveis

1. **Webhook público** para testes.

2. **Prints do fluxo N8N**.

3. **Repositório GitHub** contendo:
   
   - README
   
   - Scripts n8n


