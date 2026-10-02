# 🐛 Relatório de Bugs — Supermercado Online

Este documento reúne os bugs encontrados durante os testes funcionais, exploratórios e de API.

---

## BUG-001

**Título:** Produto excluído no Admin continua contando no carrinho e no badge

**Severidade:** Média

**Descrição:**
Ao excluir um produto no painel Admin, o item permanece no carrinho do cliente, mantendo o badge e o contador desatualizados. Ao abrir o modal do carrinho, o item excluído não aparece na lista (pois o produto não existe mais), mas o badge continua somando a quantidade e o total do carrinho fica inconsistente.

**Passos para reproduzir:**
1. Na vitrine, adicionar o produto "Arroz" ao carrinho (clicar "+" 3 vezes).
2. Verificar que o badge do carrinho mostra 3.
3. Clicar no ícone ⚙️ e fazer login com a senha de admin.
4. Na aba Produtos, clicar no ícone 🗑️ do produto "Arroz" e confirmar a exclusão.
5. Clicar em "‹ Voltar" para retornar à vitrine.
6. Observar o badge do carrinho no topo da tela.
7. Clicar no ícone 🛒 para abrir o modal do carrinho.

**Resultado esperado:**
Ao excluir um produto, o carrinho deveria ser atualizado automaticamente, removendo o item excluído. O badge deveria voltar a 0 e o total do carrinho deveria refletir apenas produtos existentes.

**Resultado obtido:**
O badge continua mostrando 3, mesmo com o produto excluído. Ao abrir o modal do carrinho, a lista aparece vazia (ou sem o Arroz), mas o badge ainda conta o item. Há inconsistência entre o badge e o conteúdo real do carrinho.

**Frequência:** Sempre

**Causa provável:**
A função `updateCartBadge()` soma `item.qty` de todos os itens do carrinho sem validar se o produto ainda existe em `products`. Já `getCartTotal()` e `sendOrder()` ignoram produtos inexistentes, gerando a inconsistência.

**Ambiente:** Chrome, Windows/Android — versão local

---

## BUG-002

**Título:** Senha do administrador exposta em texto puro no Console do navegador

**Severidade:** Crítica

**Descrição:**
A variável global `systemConfig` armazena a senha do administrador em texto puro e fica acessível a qualquer usuário através do Console do navegador (F12). Além disso, a senha é gravada no Firestore sem qualquer criptografia.

**Passos para reproduzir:**
1. Abrir o app no navegador.
2. Apertar F12 para abrir o DevTools.
3. Ir na aba Console.
4. Digitar: `systemConfig`
5. Pressionar Enter.

**Resultado esperado:**
A senha do administrador não deveria estar acessível no front-end nem ser armazenada em texto puro. O ideal é usar autenticação real (Firebase Auth) com hash de senha.

**Resultado obtido:**
A senha do admin aparece em texto puro no Console, junto com o número de WhatsApp real.

**Frequência:** Sempre

**Impacto:**
Qualquer usuário consegue obter a senha do admin e assumir o controle do painel administrativo. É uma falha de segurança grave.

**Ambiente:** Chrome, Windows/Android — versão local

---

## BUG-004

**Título:** Firestore acessível publicamente sem autenticação (leitura de dados)

**Severidade:** Crítica

**Descrição:**
A API REST do Firestore está respondendo a requisições GET sem exigir nenhum tipo de autenticação. Qualquer pessoa, de qualquer lugar, pode ler os dados do banco de dados do app, incluindo produtos e, potencialmente, pedidos de clientes e a senha do administrador.

**Passos para reproduzir:**
1. Abrir o Postman (web ou desktop).
2. Criar uma nova requisição HTTP.
3. Selecionar o método GET.
4. Colar a URL:
   `https://firestore.googleapis.com/v1/projects/rifazap-2b2ba/databases/(default)/documents/supermercado/produtos`
5. Clicar em Send.

**Resultado esperado:**
A API deveria retornar 401 Unauthorized ou 403 Forbidden, bloqueando o acesso sem autenticação.

**Resultado obtido:**
A API retornou status 200 OK com todos os dados dos produtos expostos em JSON, sem exigir login, token ou chave de API.

**Frequência:** Sempre

**Impacto:**
Exposição total dos dados do banco. Viola a LGPD e permite que qualquer pessoa leia, e potencialmente altere, dados sensíveis, incluindo a senha do administrador.

**Ambiente:** Postman — endpoint Firestore REST API — projeto `rifazap-2b2ba`

---

## 📊 Resumo

| ID | Título | Severidade | Status |
|---|---|---|---|
| BUG-001 | Produto excluído continua no carrinho | Média | Aberto |
| BUG-002 | Senha do admin exposta no Console | Crítica | Aberto |
| BUG-004 | Firestore acessível sem autenticação | Crítica | Aberto |

> **Nota:** o BUG-003 não foi registrado porque o teste de persistência do carrinho passou.
> Adiciona relatório de bugs
