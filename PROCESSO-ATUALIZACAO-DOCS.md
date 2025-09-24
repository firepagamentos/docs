# Processo de Atualização da Documentação Fire

## ⚠️ CHECKLIST OBRIGATÓRIO

### Ao criar ou modificar endpoints na API:

#### 1. ✅ **Arquivo MDX** (`/api-reference/[modulo]/[endpoint].mdx`)
- [ ] Criar/atualizar arquivo `.mdx` com documentação completa
- [ ] Exemplos de request/response atualizados
- [ ] Códigos de erro documentados
- [ ] Casos de uso e exemplos práticos

#### 2. ✅ **OpenAPI JSON** (`/api-reference/openapi.json`)
- [ ] **Endpoint**: Adicionar/atualizar rota no `paths`
- [ ] **Schemas**: Criar/atualizar schemas no `components.schemas`
- [ ] **Exemplos**: Garantir que exemplos estão corretos
- [ ] **Códigos de resposta**: Documentar todos os status codes

#### 3. ✅ **Navegação** (`/docs.json`)
- [ ] Adicionar página na navegação correta
- [ ] Verificar ordem dos itens no menu
- [ ] Testar se a página aparece no menu

#### 4. ✅ **Validação Local**
- [ ] Executar `mint dev` e verificar se funciona
- [ ] Testar exemplos de código na lateral direita
- [ ] Verificar se não há erros de JSON/sintaxe
- [ ] Navegar pelos menus e links

## 🔧 **Por que isso é crítico?**

### **O que acontece se eu esquecer:**

1. **Só MDX**: Documentação fica incompleta na lateral direita
2. **Só OpenAPI**: Página não existe, mas exemplos funcionam
3. **Não atualizar navegação**: Usuário não encontra a documentação
4. **Exemplos desatualizados**: Desenvolvedores implementam errado

### **Mintlify funciona assim:**
- **MDX**: Conteúdo principal da página
- **OpenAPI JSON**: Exemplos interativos na lateral direita
- **docs.json**: Navegação e estrutura do menu

## 📝 **Exemplo de Fluxo Completo**

### Cenário: Novo campo `consultedAt` no `/v1/account/balance`

#### 1. **Arquivo MDX** ✅
```markdown
# /api-reference/account/balance.mdx
"consultedAt": "2024-01-15T10:30:45.123Z"
```

#### 2. **OpenAPI JSON** ✅
```json
"consultedAt": {
  "type": "string",
  "format": "date-time",
  "description": "Timestamp ISO 8601 de quando o saldo foi consultado",
  "example": "2024-01-15T10:30:45.123Z"
}
```

#### 3. **Navegação** (se novo endpoint) ✅
```json
"pages": [
  "api-reference/account/balance",
  "api-reference/account/webhook"
]
```

## 🚨 **Comandos de Validação**

```bash
# 1. Navegar para docs
cd /Users/lucastorress/Git/firebanking-services/docs-fire

# 2. Executar preview local
mint dev

# 3. Abrir no navegador
open http://localhost:3000

# 4. Validar JSON (se houver dúvidas)
cat api-reference/openapi.json | python -m json.tool > /dev/null && echo "✅ JSON válido"
```

## 📋 **Template para Novos Endpoints**

### Arquivo MDX mínimo:
```markdown
---
title: 'Nome do Endpoint'
openapi: 'POST /v1/endpoint'
---

Descrição do endpoint...
```

### Schema OpenAPI mínimo:
```json
"/v1/endpoint": {
  "post": {
    "tags": ["Módulo"],
    "summary": "Título",
    "description": "Descrição",
    "security": [{ "apiKeyAuth": [] }],
    "responses": {
      "200": {
        "description": "Sucesso",
        "content": {
          "application/json": {
            "schema": {
              "$ref": "#/components/schemas/EndpointResponse"
            }
          }
        }
      }
    }
  }
}
```

## ⏰ **Quando aplicar este processo:**

- ✅ **Novo endpoint criado**
- ✅ **Campo adicionado/removido**
- ✅ **Mudança de contrato de API**
- ✅ **Novos códigos de erro**
- ✅ **Alteração de URL/método HTTP**

---

**💡 Lembre-se:** A documentação é tão importante quanto o código!