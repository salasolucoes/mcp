# @sala/mcp

MCP server **sala-boost** — `sala_info`, `sala_schema`, `sala_query`, `sala_logs` para `salaab/framework` (e derivados sem Laravel puro).

Extraído de `mcp/sala` do framework — mesmo fluxo do `sala/console`.

## Instalação

```bash
npm install -D @sala/mcp
# ou
npm install -g @sala/mcp
```

Build (gera `dist/`):

```bash
npm run build
```

## Uso — MCP (Code / OpenCode / Claude)

### Opencode

`opencode.json`:

```json
{
  "mcp": {
    "sala-boost": {
      "type": "local",
      "command": ["node", "node_modules/@sala/mcp/dist/index.js"],
      "enabled": true
    }
  }
}
```

### MCP genérico (`.mcp.json` / Cursor / Claude)

```json
{
  "mcpServers": {
    "sala-boost": {
      "command": "node",
      "args": ["node_modules/@sala/mcp/dist/index.js"]
    }
  }
}
```

Ou via binário publicado (após `npm install`):

```json
{
  "mcpServers": {
    "sala-boost": {
      "command": "sala-mcp"
    }
  }
}
```

### Variável opcional

- `SALA_PROJECT_ROOT` — força a raiz do projeto (caso o auto-detecção por `composer.json`/`phinx.php`/`config/database.php` não alcance). Ex: `SALA_PROJECT_ROOT=/caminho/do/projeto node node_modules/@sala/mcp/dist/index.js`

## Tools

| Tool | Descrição |
|---|---|
| `sala_info` | PHP + Illuminate/BladeOne/Phinx, DB driver, models Eloquent — Application Info |
| `sala_schema` | `SHOW TABLES` / `DESCRIBE <table>` (fallback: lista de migrations) |
| `sala_query` | `SELECT` read-only via Capsule (bloqueia DROP/DELETE sem `write:true`) |
| `sala_logs` | Tail de `storage/logs` (últimas N linhas) |

## Framework consumidor

No framework (`salaab/framework`), o `mcp/sala` local foi removido — o MCP vem do pacote. Veja o `README` do framework para a integração.

## Requisitos

- Node >= 18
- PHP + `salaab/framework` na raiz detectada (para `sala_schema`/`sala_query`)

## Licença

MIT
