# 🔍 Teste Exploratório — Supermercado Online

Sessão de teste exploratório realizada sem roteiro fixo, com o objetivo de encontrar comportamentos inesperados.

**Duração:** 30 minutos
**Ambiente:** Chrome, Windows
**Técnica:** Exploração livre + inspeção via DevTools

---

## Ações testadas

| # | Ação | Resultado |
|---|---|---|
| 1 | Cadastrar produto com nome de 500 caracteres | Aceito sem validação de tamanho (comportamento inesperado) |
| 2 | Cadastrar produto com preço negativo (-10) | Bloqueado pela validação `price <= 0` |
| 3 | Cadastrar produto com preço gigante (999999999) | Aceito sem validação de limite |
| 4 | Forçar no Console: `cart = [{ id: 1, qty: 0 }]` | Carrinho aceita quantidade 0 (inconsistência) |
| 5 | Abrir o app em duas abas e adicionar item em uma | A outra aba não atualiza automaticamente |
| 6 | Forçar no Console: `products = null` e clicar em "+" | App quebra com erro no Console |
| 7 | Excluir produto que está no carrinho | Bug BUG-001 confirmado |
| 8 | Editar produto apagando o preço | Preço vira 0 sem validação (BUG-003 candidato) |
| 9 | Editar produto apagando o nome | Produto fica sem nome (BUG-005 candidato) |
| 10 | Enviar pedido e verificar formulário | Campos permanecem preenchidos após envio |

---

## Achados adicionais (não categorizados como bug principal)

### A01 — Falta de validação de tamanho em nomes
O campo "Nome do produto" aceita textos arbitrariamente longos, sem limite. Pode quebrar o layout em telas pequenas.

### A02 — Falta de validação de preço máximo
O campo "Preço" aceita valores como 999999999 sem aviso. Isso pode gerar totais absurdos no carrinho.

### A03 — Quantidade 0 aceita no carrinho via Console
Normalmente o usuário não consegue fazer isso pela UI, mas via Console o app aceita. Não é um bug crítico, mas mostra falta de validação na camada de dados.

### A04 — Duas abas abertas não sincronizam
O app usa listeners do Firestore, mas o carrinho está só no `localStorage` de cada aba. Isso é comportamento esperado, mas vale documentar como limitação.

### A05 — App quebra com `products = null`
Falta de tratamento de erro. Se `products` for nulo, o `renderCatalog()` quebra.

---

## Recomendações

1. Adicionar validação de tamanho máximo nos campos de texto.
2. Adicionar validação de preço máximo (ex.: R$ 100.000).
3. Validar quantidade mínima 1 na camada de dados.
4. Adicionar tratamento de erro em `renderCatalog()`.
5. Considerar sincronizar o carrinho via Firestore para múltiplas abas.
6. Adiciona teste exploratório
