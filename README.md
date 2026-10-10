# ImaginArt Studio 3D

Aplicação web local para acompanhar filamentos, custos de produtos, encomendas, produção, pagamentos e relatórios do ImaginArt Studio 3D.

## Requisitos

- Node.js 20 ou superior e npm.
- Navegador moderno com IndexedDB habilitado.

## Executar no VS Code

Abra a pasta do projeto no VS Code e, no terminal integrado, execute:

```powershell
npm install
npm run dev
```

O Vite informa a URL local no terminal (normalmente `http://localhost:5173`). Para compilar e testar:

```powershell
npm test
npm run build
npm run preview
```

## Funcionalidades

- Dashboard com período selecionável, faturamento, custos, lucro estimado, valores recebidos/a receber, indicadores de produção, gráficos e alertas de prazo/estoque/pagamento.
- Cadastro, edição e exclusão protegida de filamentos; custo por grama, quantidade disponível, nível mínimo e histórico de compras.
- Catálogo de produtos com vários filamentos, consumo por unidade, energia, acabamento, embalagem, custos adicionais, preço, lucro, margem e markup.
- Encomendas com código automático, cliente, produto de catálogo ou personalizado, prazo, custo estimado, histórico de etapas, Kanban arrastável e pagamento inicial opcional.
- Baixa de material transacional e idempotente quando a encomenda entra em impressão. Estoque insuficiente impede a mudança de etapa e não deixa baixas parciais.
- Pagamentos parciais, estornos registrados no histórico, formas de pagamento, descontos, taxas e distinção entre vendido, recebido e saldo.
- Vendas e financeiro separados, relatórios PDF paginados em A4 paisagem de encomendas/financeiro, produtos/custos e estoque.
- Preferências de expediente, dias de trabalho, energia, potência e margem de segurança; backup JSON e restauração; notificação local somente com autorização e enquanto o navegador está aberto.
- Interface responsiva em português brasileiro, valores em reais e datas formatadas para `America/Sao_Paulo`.

## Persistência e backup

Cadastros são gravados em IndexedDB pelo Dexie e permanecem após atualizar ou reabrir o navegador no mesmo perfil e dispositivo. Não há conta, servidor ou sincronização entre dispositivos. Os relatórios PDF são gerados localmente no momento da exportação; o backup JSON em **Configurações** contém os dados necessários para restaurar as tabelas e preferências. Restaurar substitui os registros locais atuais.

Exporte backups em local seguro com frequência. Limpar os dados do site/perfil do navegador remove a base local.

## Limitações conhecidas

- Agenda informa uma estimativa de início baseada no expediente, duração e margem de segurança, mas ainda não faz reserva automática de impressoras, manutenção, períodos indisponíveis ou nivelamento da carga de várias encomendas. Confira a capacidade antes de prometer prazos.
- O custo estimado é capturado na encomenda; alterações posteriores no catálogo não reescrevem esse histórico. Vendas podem ser filtradas por data, produto e forma de pagamento; categorias e comparações avançadas entre períodos ainda não estão disponíveis.
- Cancelar uma encomenda mantém os recebimentos/estornos no histórico. Se o material já foi consumido, o cancelamento não o devolve automaticamente ao estoque.
- Notificações são locais e dependem da permissão do navegador; não são enviadas com o app fechado.
- O custo de acabamento monetário é informado manualmente. Tempo de acabamento e impressão são usados separadamente para estimativas operacionais.

## Testes

`npm test` cobre fórmulas de custo, energia, margem/markup, divisão por zero, pagamentos parciais, estornos, prazo em expediente, baixa de estoque atômica/idempotente e geração dos três PDFs. `npm run build` executa TypeScript e gera o bundle de produção.
