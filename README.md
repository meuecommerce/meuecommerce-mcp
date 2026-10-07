<p align="center">
  <img src="logo.png" alt="Meu Ecommerce" width="120" height="120">
</p>

# Meu Ecommerce MCP

Hosted remote MCP server that connects AI agents to Brazil's Correios through a Meu Ecommerce store: shipping quotes (frete), tracking (rastreio) and shipping labels (etiqueta), in a single connection.

```text
https://app.meuecommerce.com.br/mcp
```

- **Transport:** Streamable HTTP
- **Auth:** OAuth (Authorization Code + PKCE S256, dynamic client registration) or a store secret key
- **Docs (Portuguese):** [dev.meuecommerce.com.br/docs/mcp](https://dev.meuecommerce.com.br/docs/mcp)

This repository only holds the server's public description (`server.json`), its logo and this guide. The server is a hosted service: there is nothing to install.

## Tools

| Tool | What it does |
| --- | --- |
| [`get_shipping_rates`](https://dev.meuecommerce.com.br/docs/mcp/ferramentas/get-shipping-rates) | Quotes Correios shipping for an order to a destination CEP (postal code) |
| [`track_shipment`](https://dev.meuecommerce.com.br/docs/mcp/ferramentas/track-shipment) | Returns the tracking events of Correios parcels |
| [`generate_label`](https://dev.meuecommerce.com.br/docs/mcp/ferramentas/generate-label) | Creates the Correios pre-posting (pré-postagem) and generates the label |
| [`get_label_pdf`](https://dev.meuecommerce.com.br/docs/mcp/ferramentas/get-label-pdf) | Downloads the PDF of a label already generated |

Available tools depend on the store's credentials and setup. Connecting does not unlock every operation: quotes need the store's origin CEP, shipping services and plan configured; labels also need the merchant's own authenticated Correios contract.

## Connect

- **OAuth clients (recommended, e.g. Claude):** add a remote MCP server with the URL above and complete the store login and authorization in the browser.
- **Clients that accept headers:** use Streamable HTTP and send the store secret key as `Authorization: Bearer mk_YOUR_KEY`. Keep it in a secrets manager, never in prompts, repositories or browser code.

OAuth discovery starts at `https://app.meuecommerce.com.br/.well-known/oauth-protected-resource/mcp`. A `401` before authorization is part of discovery.

---

## Português

Servidor MCP remoto que conecta agentes de IA à sua loja Meu Ecommerce: cotação de frete, rastreamento de objetos e etiquetas dos Correios, em uma única conexão.

### Ferramentas

| Ferramenta | O que faz | Capacidade |
| --- | --- | --- |
| [`get_shipping_rates`](https://dev.meuecommerce.com.br/docs/mcp/ferramentas/get-shipping-rates) | Cota o frete de um pedido para um CEP de destino | [Fretes e cotações](https://dev.meuecommerce.com.br/docs/capacidades/fretes) |
| [`track_shipment`](https://dev.meuecommerce.com.br/docs/mcp/ferramentas/track-shipment) | Consulta os eventos de rastreamento de objetos | [Rastreamento](https://dev.meuecommerce.com.br/docs/capacidades/rastreamento) |
| [`generate_label`](https://dev.meuecommerce.com.br/docs/mcp/ferramentas/generate-label) | Cria a pré-postagem e gera a etiqueta | [Etiquetas e postagens](https://dev.meuecommerce.com.br/docs/capacidades/etiquetas) |
| [`get_label_pdf`](https://dev.meuecommerce.com.br/docs/mcp/ferramentas/get-label-pdf) | Baixa o PDF de uma etiqueta já gerada | [Etiquetas e postagens](https://dev.meuecommerce.com.br/docs/capacidades/etiquetas) |

As ferramentas disponíveis dependem da credencial e da configuração da loja. Conectar o MCP não libera todas as operações:

- **Cotação:** CEP de origem, serviços de envio e acesso ao plano configurados no painel.
- **Etiquetas:** além disso, contrato próprio dos Correios autenticado e integração de etiquetas habilitada.

Configure a loja em [app.meuecommerce.com.br/start](https://app.meuecommerce.com.br/start).

### Conectar

#### Clientes com OAuth (recomendado)

1. Abra a área de conectores ou servidores MCP do seu cliente (por exemplo, Claude).
2. Adicione um servidor remoto chamado **Meu Ecommerce** com a URL `https://app.meuecommerce.com.br/mcp`.
3. Conclua o login e a autorização da loja no navegador.
4. Volte ao cliente e confira as ferramentas disponíveis.

#### Clientes que aceitam headers

Configure o transporte Streamable HTTP e envie a chave secreta da loja:

```http
Authorization: Bearer mk_SUA_CHAVE
```

Guarde a chave no gerenciador de segredos do ambiente. Nunca a inclua em prompts, repositórios ou código executado no navegador.

#### Primeiro teste

> Cote o envio para o CEP 20040-002 de uma camiseta de algodão, quantidade 1, preço unitário R$ 89,90 e peso unitário 0,3 kg. Mostre os serviços, preços e prazos retornados.

Guia completo: [Conecte seu agente](https://dev.meuecommerce.com.br/docs/mcp/conectar).

### Descoberta OAuth

- Recurso protegido: `https://app.meuecommerce.com.br/.well-known/oauth-protected-resource/mcp`
- Servidor de autorização: `https://app.meuecommerce.com.br/.well-known/oauth-authorization-server`

Um `401` antes da autorização faz parte da descoberta.

---

## License / Licença

The documentation and files in this repository are under the [MIT License](LICENSE). The server's source code is not distributed here.

A documentação e os arquivos deste repositório estão sob a [licença MIT](LICENSE). O código do servidor não é distribuído aqui.
