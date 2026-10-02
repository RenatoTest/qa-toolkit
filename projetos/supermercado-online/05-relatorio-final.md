# 📋 Relatório Final de Testes — Supermercado Online

## 1. Informações gerais

| Campo | Valor |
|---|---|
| Projeto | Supermercado Online |
| Versão testada | Local (index.html) |
| Responsável | Renato |
| Data | [preencher] |
| Ambiente | Chrome, Windows/Android |

## 2. Escopo

### O que foi testado
- Catálogo de produtos
- Carrinho de compras
- Envio de pedido via WhatsApp
- Painel administrativo (login, produtos, pedidos, configurações)
- API REST do Firestore
- Segurança básica (exposição de dados)

### O que NÃO foi testado
- Testes de performance e carga
- Testes em múltiplos navegadores (apenas Chrome)
- Testes de acessibilidade
- Testes em dispositivos móveis reais

## 3. Resumo dos resultados

| Métrica | Valor |
|---|---|
| Casos de teste executados | 10 |
| Casos com sucesso | 7 |
| Casos com falha | 3 |
| Bugs encontrados | 3 |
| Bugs críticos | 2 |
| Bugs de severidade média | 1 |

## 4. Lista de bugs

| ID | Título | Severidade |
|---|---|---|
| BUG-002 | Senha do admin exposta no Console | Crítica |
| BUG-004 | Firestore acessível sem autenticação | Crítica |
| BUG-001 | Produto excluído continua no carrinho | Média |

## 5. Considerações finais

### O sistema está pronto para produção?
**Não.** Os bugs críticos de segurança (BUG-002 e BUG-004) impedem o uso em produção. Qualquer pessoa consegue ler os dados do banco e obter a senha do admin.

### Riscos mais graves
1. **Exposição total do banco de dados** — viola LGPD e permite adulteração de dados.
2. **Senha do admin em texto puro** — qualquer usuário se torna administrador.
3. **Sem autenticação real** — o app depende apenas de uma senha comparada no front-end.

### Recomendações prioritárias
1. **Urgente:** Fechar as regras do Firestore no Console do Firebase.
2. **Urgente:** Implementar Firebase Authentication.
3. **Alta:** Remover a senha do front-end e do Firestore.
4. **Média:** Corrigir a lógica do carrinho para remover itens excluídos.
5. **Média:** Adicionar validações de tamanho e valor nos formulários.

## 6. Anexos

- `02-bugs.md` — Detalhamento dos bugs
- `03-exploratorio.md` — Achados do teste exploratório
- `04-api.md` — Testes de API
- `evidencias/` — Prints e vídeos (a adicionar)
- Adiciona relatório final de testes
