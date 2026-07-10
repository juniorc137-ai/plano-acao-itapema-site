# Plano de Ação Estratégico — Dashboard de Monitoramento (Itapema/SC)

Aplicativo web estático (HTML + CSS + JavaScript puro, sem dependências de build) para acompanhamento contínuo do plano de ação estratégico de assessoria de gestão em saúde, organizado em 4 eixos e 12 ações monitoráveis.

## Publicar no GitHub Pages

1. Crie um repositório novo (ou use um existente) e envie os arquivos deste diretório mantendo `index.html` na raiz:
   ```bash
   git init
   git add index.html README.md
   git commit -m "Dashboard do plano de ação estratégico — Itapema/SC"
   git branch -M main
   git remote add origin https://github.com/<seu-usuario>/<seu-repositorio>.git
   git push -u origin main
   ```
2. No GitHub, acesse **Settings → Pages**.
3. Em **Source**, selecione a branch `main` e a pasta `/ (root)`.
4. Salve. O site fica disponível em alguns minutos em:
   `https://<seu-usuario>.github.io/<seu-repositorio>/`

Nenhum passo de build, servidor ou variável de ambiente é necessário — é um arquivo HTML autocontido.

## Funcionalidades

- **Faixa de sinais vitais**: leitura instantânea do status agregado dos 4 eixos (Crítico / Atenção / Em andamento / Concluído).
- **Indicadores consolidados (KPIs)**: total de ações, % de atingimento geral, eixos em situação crítica, prazo mais próximo.
- **Barras de distância-até-a-meta**: cada ação mostra o percentual atual preenchido sobre uma trilha de 0–100%, com marcador na posição da meta — tornando o GAP (p.p.) visualmente explícito.
- **Distribuição de status** (gráfico de rosca) recalculada em tempo real.
- **12 ações editáveis**, agrupadas por eixo em formato expansível: descrição do objetivo, ação específica, indicador, percentual atual, meta, datas de início/término, responsável, prazo e observações/evidências.
- **Busca, filtros** (eixo, status, responsável) **e ordenação** (maior GAP, menor atingimento, código).
- **Exportação em CSV** e **impressão** de relatório.
- **Persistência local automática** via `localStorage` do navegador — os dados preenchidos permanecem salvos entre visitas, sem necessidade de backend.

## Escopo e limitações da persistência

Os dados são salvos **no navegador de cada usuário** (`localStorage`), não em um banco de dados compartilhado. Isso significa que:

- Os dados persistem entre sessões no mesmo navegador/dispositivo.
- Diferentes pessoas acessando o link não compartilham as mesmas edições entre si.
- Limpar o cache/dados de navegação do navegador apaga o conteúdo salvo (use o botão **Exportar CSV** periodicamente como backup).

Para uso colaborativo por múltiplos membros da equipe de assessoria com sincronização real, seria necessário um backend leve (ex.: Firebase, Supabase, planilha do Google via API, ou um endpoint próprio) — fora do escopo de um site estático no GitHub Pages, mas posso ajudar a implementar caso a equipe tenha essa necessidade.

## Fundamentação metodológica

O desenho de monitoramento por eixos, indicadores e metas segue os princípios do Planejamento Estratégico Situacional (Matus) e as diretrizes de monitoramento e avaliação do Ministério da Saúde / PlanejaSUS. As fórmulas de cálculo replicam exatamente a lógica da planilha de origem:

- `GAP (p.p.) = Meta (%) − Percentual atual (%)`
- `% de atingimento = MIN(Percentual atual / Meta, 100%)`
- `Status`: Concluído (≥100%) · Em andamento (≥70%) · Atenção (≥30%) · Crítico (<30%)

## Estrutura do repositório

```
.
├── index.html   # aplicativo completo (HTML + CSS + JS)
└── README.md
```
