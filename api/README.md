# ClientFlow — API de desenvolvimento

API REST local para o projeto de portfólio **ClientFlow CRM**. Ela permite desenvolver o Front-end em React sem precisar implementar um backend.

## Arquivos

- `db.json`: base de dados utilizada pela API.
- `db.seed.json`: cópia original para restaurar os dados de demonstração.
- `ClientFlow-CRM-API.postman_collection.json`: coleção Postman com requests e testes básicos.

## Iniciar a API

É necessário ter Node.js instalado. Abra o terminal nesta pasta e execute:

```bash
npx json-server@0.17.4 --watch db.json --port 3001
```

Na primeira execução, o `npx` poderá solicitar autorização para baixar o JSON Server. Confirme e aguarde a inicialização.

A API ficará disponível em `http://localhost:3001`. Mantenha esse terminal aberto enquanto desenvolve o React.

## Importar no Postman

1. Abra o Postman.
2. Clique em **Import**.
3. Selecione `ClientFlow-CRM-API.postman_collection.json`.
4. Abra a coleção **ClientFlow CRM API**. A variável `baseUrl` já está configurada como `http://localhost:3001`.
5. Execute os requests para validar a API.

## Endpoints disponíveis

| Método | Endpoint | Objetivo |
|---|---|---|
| GET | `/dashboard/1` | Indicadores do dashboard |
| GET | `/customers` | Listagem de clientes |
| GET | `/customers?_page=1&_limit=8` | Paginação |
| GET | `/customers?q=mariana` | Busca textual |
| GET | `/customers?status=active` | Filtro por status |
| GET | `/customers/:id` | Detalhes do cliente |
| POST | `/customers` | Criar cliente |
| PATCH | `/customers/:id` | Atualizar cliente |
| DELETE | `/customers/:id` | Excluir cliente |
| GET | `/activities` | Listar atividades |
| GET | `/activities?customerId=1` | Atividades de um cliente |
| POST | `/activities` | Criar atividade |

## Paginação, busca e filtros

O JSON Server 0.17.4 oferece parâmetros como `_page`, `_limit`, `_sort`, `_order` e `q`. Também permite filtrar por propriedades, por exemplo `status=active`. Quando `_limit` é utilizado, consulte o header `X-Total-Count` para obter o total de registros.

Exemplo:

```text
GET http://localhost:3001/customers?_page=1&_limit=8&_sort=createdAt&_order=desc
```

## Observações importantes

- Esta é uma API de desenvolvimento simulada pelo JSON Server, não um backend de produção.
- As operações POST, PATCH e DELETE alteram o arquivo `db.json`.
- Para restaurar os dados originais, pare o servidor e copie `db.seed.json` sobre `db.json` (`cp db.seed.json db.json` no Linux/macOS).
- Não há autenticação real, autorização ou regras de negócio no servidor. A ideia inicial é praticar React, consumo de API, estados de interface, formulários, paginação e testes.
- Os indicadores de `/dashboard/1` são dados demonstrativos estáticos e não são recalculados automaticamente a partir dos clientes.
- A API é local. Para acessá-la a partir do Vite/React, utilize a URL `http://localhost:3001`.
