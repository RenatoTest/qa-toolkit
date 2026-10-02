# 🗺️ Mapeamento do Sistema — Supermercado Online

## 1. Visão geral

O app é uma aplicação web de página única (SPA simples) que simula um supermercado online. Ele se comunica com o Firestore (Firebase) para persistir produtos, pedidos e configurações.

## 2. Telas e seções identificadas

| # | Nome | Tipo | Como acessar |
|---|---|---|---|
| 1 | Vitrine (catálogo) | Tela | Tela inicial do app |
| 2 | Painel Admin | Tela | Clicar no ícone ⚙️ + senha |
| 3 | Modal de login Admin | Modal | Ao clicar no ⚙️ |
| 4 | Modal do Carrinho | Modal | Ao clicar no 🛒 |
| 5 | Modal de Edição de Produto | Modal | Admin → Produtos → ✏️ |
| 6 | Modal de Novo Produto | Modal | Admin → Novo Produto |

## 3. Abas do Painel Admin

- 📦 Produtos
- 📋 Pedidos
- ⚙️ Configurações

> Observação: apenas essas três são abas verdadeiras. Os modais (login, carrinho, edição) **não** são abas.

## 4. Elementos interativos (clicáveis)

### Tela Vitrine
- Botão 🛒 (abre carrinho)
- Botão ⚙️ (abre login admin)
- Campo de busca (input)
- Botão "+" em cada produto
- Botão "−" em cada produto

### Modal do Carrinho
- Botões "+" e "−" por item
- Botão "✕" para remover item
- Botão "Enviar pedido via WhatsApp"
- Botão "Fechar"

### Painel Admin
- Botão "‹ Voltar"
- Botão "➕ Novo Produto"
- Abas Produtos / Pedidos / Configurações
- Botões ✏️ (editar) e 🗑️ (excluir) por produto
- Botão "Salvar Configurações"

## 5. Elementos visuais (não clicáveis)

- Logo "🛒 Supermercado Online"
- Card de cada produto (container)
- Emoji, nome e preço de cada produto
- Contador de quantidade
- Badge do carrinho (número vermelho)
- Mensagens de toast (sucesso/erro)

## 6. Campos de formulário

### Modal do Carrinho
| Campo | Tipo | Obrigatório |
|---|---|---|
| Nome completo | texto | Sim |
| Endereço completo | textarea | Sim |
| Forma de pagamento | select | Sim |
| Observações | textarea | Não |

### Modal de Produto (criar/editar)
| Campo | Tipo | Obrigatório |
|---|---|---|
| Emoji | texto | Não |
| Nome | texto | Sim |
| Preço | número | Sim |

## 7. Fluxo principal do usuário

Vitrine → adiciona produtos ao carrinho → abre modal do carrinho → preenche dados → clica em "Enviar pedido via WhatsApp" → WhatsApp abre com a mensagem → pedido é salvo no Firestore → aparece no Painel Admin → Pedidos

## 8. Fluxo do administrador

Vitrine → clica no ⚙️ → digita senha → acessa Painel Admin → gerencia produtos, pedidos e configurações → clica em "‹ Voltar"

## 9. Persistência de dados

| Dado | Onde fica salvo |
|---|---|
| Produtos | Firestore → coleção `supermercado`, doc `produtos` |
| Pedidos | Firestore → coleção `supermercado`, doc `pedidos` |
| Configurações | Firestore → coleção `supermercado`, doc `config` |
| Carrinho do cliente | `localStorage` do navegador |
Adiciona mapeamento do sistema
