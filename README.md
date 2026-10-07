<p align="center">
  <img src="logo.png" alt="Meu Ecommerce" width="120" height="120">
</p>

# Meu Ecommerce MCP

Servidor MCP remoto que conecta agentes de IA à sua loja Meu Ecommerce: cotação de frete, rastreamento de objetos e etiquetas dos Correios, em uma única conexão.

```text
https://app.meuecommerce.com.br/mcp
```

- **Transporte:** Streamable HTTP
- **Autenticação:** OAuth (Authorization Code + PKCE S256, registro dinâmico de clientes) ou chave secreta da loja
- **Documentação completa:** [dev.meuecommerce.com.br/docs/mcp](https://dev.meuecommerce.com.br/docs/mcp)

Este repositório contém apenas a descrição pública do servidor (`server.json`), o logo e este guia. O servidor é um serviço hospedado; não há nada para instalar.

## Ferramentas

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

## Conectar

### Clientes com OAuth (recomendado)

1. Abra a área de conectores ou servidores MCP do seu cliente (por exemplo, Claude).
2. Adicione um servidor remoto chamado **Meu Ecommerce** com a URL `https://app.meuecommerce.com.br/mcp`.
3. Conclua o login e a autorização da loja no navegador.
4. Volte ao cliente e confira as ferramentas disponíveis.

### Clientes que aceitam headers

Configure o transporte Streamable HTTP e envie a chave secreta da loja:

```http
Authorization: Bearer mk_SUA_CHAVE
```

Guarde a chave no gerenciador de segredos do ambiente. Nunca a inclua em prompts, repositórios ou código executado no navegador.

### Primeiro teste

> Cote o envio para o CEP 20040-002 de uma camiseta de algodão, quantidade 1, preço unitário R$ 89,90 e peso unitário 0,3 kg. Mostre os serviços, preços e prazos retornados.

Guia completo: [Conecte seu agente](https://dev.meuecommerce.com.br/docs/mcp/conectar).

## Descoberta OAuth

- Recurso protegido: `https://app.meuecommerce.com.br/.well-known/oauth-protected-resource/mcp`
- Servidor de autorização: `https://app.meuecommerce.com.br/.well-known/oauth-authorization-server`

Um `401` antes da autorização faz parte da descoberta.

## English

**Meu Ecommerce MCP** is a hosted remote MCP server for Brazilian merchants on Meu Ecommerce. It lets AI agents quote shipping rates, track parcels and generate Correios shipping labels for the merchant's store.

- **Endpoint:** `https://app.meuecommerce.com.br/mcp` (Streamable HTTP)
- **Auth:** OAuth (Authorization Code + PKCE) and dynamic client registration, or a store secret key sent as `Authorization: Bearer`
- **Tools:** `get_shipping_rates`, `track_shipment`, `generate_label`, `get_label_pdf`
- **Docs (Portuguese):** [dev.meuecommerce.com.br/docs/mcp](https://dev.meuecommerce.com.br/docs/mcp)

Available tools depend on the store's credentials and setup. Label tools require the merchant's own Correios contract.

## Licença

A documentação e os arquivos deste repositório estão sob a [licença MIT](LICENSE). O código do servidor não é distribuído aqui.
