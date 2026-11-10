# 🏗️ Cockpit de Acompanhamento Físico e Prazos — Projeto São Luís

Dashboard executivo e interativo para gestão visual do cronograma de obras civis, conectando a planta de situação (layout de implantação) aos apontamentos de produção e avanço físico exportados do **Prevision**.

Aplicação autônoma *Single-Page* (HTML5, SVG e JavaScript Vanilla), projetada para rodar diretamente no navegador e ser hospedada gratuitamente via **GitHub Pages**, com processamento 100% *client-side* (sem necessidade de servidores ou bancos de dados dedicados).

---

## 🎯 Objetivo

Eliminar o atrito de leitura de cronogramas extensos em planilhas ou diagramas de Gantt estáticos. Ao clicar em qualquer bloco de casas na planta de implantação, o gestor de obras, engenheiro ou diretoria visualiza instantaneamente:
- O percentual consolidado de avanço físico daquela unidade;
- As atividades concluídas, em produção e atrasadas;
- A listagem detalhada de serviços pendentes classificados por criticidade de prazo.

---

## 🧭 Estrutura Física do Empreendimento

O projeto engloba **156 casas** distribuídas em **78 blocos geminados/duplos**, agrupados em 5 quadras:

| Quadra | Descrição do Setor | Unidades / Blocos | Quantidade |
| :---: | :--- | :--- | :---: |
| **Quadra E** | Malha inferior horizontal | Lotes `1 - 2` a `19 - 20` | 10 blocos (20 casas) |
| **Quadra D** | Alça vertical esquerda | Lotes `21 - 22` a `55 - 56` + `151 - 152 PCD` | 19 blocos (38 casas) |
| **Quadra C** | Alça vertical central | Lotes `57 - 58` a `91 - 92` + `153 - 154 PCD` | 19 blocos (38 casas) |
| **Quadra B** | Alça vertical direita | Lotes `93 - 94` a `127 - 128` + `155 - 156 PCD` | 19 blocos (38 casas) |
| **Quadra A** | Faixa vertical externa direita | Lotes `129 - 130` a `149 - 150` | 11 blocos (22 casas) |
| **TOTAL** | **Escopo Civil Habitacional** | **78 Lotes Mapeados** | **156 Casas** |

> **Nota:** Serviços gerais de `INFRA`, `INDIRETOS NOVOS` e `AREA COMUM` foram isolados no tratamento para que o painel reflita estritamente a linha de balanço das unidades habitacionais.

---

## 🚦 Regras de Negócio e Semáforo de Prazos

O status de cada uma das **4.946 tarefas civis** é calculado dinamicamente correlacionando o avanço realizado no campo com as datas planejadas da Linha de Base:

| Status | Critério Técnico | Cor Semafórica |
| :--- | :--- | :---: |
| **Concluído** | Avanço físico realizado igual a **100%**. | 🟢 Verde (`#10b981`) |
| **Final Atrasado** | Avanço físico realizado menor que 100% e **Data Término Planejada < Data Base**. | 🔴 Vermelho (`#ef4444`) |
| **Início Atrasado** | Avanço físico em 0% e **Data Início Planejada < Data Base**. | 🔴 Vermelho Claro (`#f87171`) |
| **Em Andamento** | Avanço físico entre 1% e 99% e **Data Base dentro do prazo planejado**. | 🟡 Amarelo/Laranja (`#f59e0b`) |
| **Não Iniciado** | Avanço físico em 0% e prazo de início ainda não atingido. | ⚪ Cinza (`#475569`) |

### Status Geral do Lote no Mapa
A cor de cada bloco na planta reflete a atividade mais crítica vinculada a ele (Hierarquia: **Atraso > Em Andamento > Não Iniciado > Concluído**). Se um lote possuir qualquer atividade com prazo estourado, ele acende imediatamente em vermelho no mapa.

---

## ⚡ Principais Recursos do Dashboard

1. **Layout Vetorial SVG com Pan & Zoom:**
   - Navegação por clique e arraste (pan) e zoom dinâmico através do scroll do mouse ou botões de controle (`+`, `−`, `↺`).
   - Tooltips instantâneos ao passar o mouse sobre cada lote com resumo de avanço e atrasos.
2. **Filtragem Cruzada Bidirecional:**
   - Filtros rápidos por **Quadra (A, B, C, D, E)** com contadores de lotes.
   - Filtros por **Status** (*⚠️ Pendentes*, *🚨 Atrasadas*, *⏳ Em Andamento*, *✅ Concluídas*).
   - Filtro por **Pacote de Trabalho** (dropdown dinâmico com os 36 pacotes de obra).
   - Campo de **busca textual** em tempo real por serviço ou número do lote.
3. **Cockpit com Gráficos Executivos (Chart.js):**
   - **Distribuição de Status:** gráfico de rosca com contagem e percentual da visão atual.
   - **Avanço Médio por Quadra:** barras comparativas do progresso físico real entre as quadras.
   - **Top Gargalos da Obra:** ranking dos pacotes com maior volume de tarefas atrasadas.
4. **Persistência e Ingestão Local de Dados:**
   - Base de **4.946 tarefas civis pré-carregada** para uso imediato sem necessidade de upload na primeira visualização.
   - Botão **"Subir Planilha Prevision (.xlsx)"**: lê arquivos exportados do Prevision diretamente na memória do navegador via SheetJS (sem trafegar dados em servidores externos).
   - Botão **"Exportar CSV"**: permite baixar a relação filtrada de tarefas para análises externas.

---

## 🛠️ Tecnologias Utilizadas

- **HTML5 & CSS3:** Interface responsiva em Dark Theme desenvolvida para telas desktop, tablets e notebooks de campo.
- **JavaScript (ES6+):** Lógica matemática de status, tratamento de dados e gerenciamento de estado sem frameworks pesados.
- **[SheetJS (xlsx.full.min.js)](https://sheetjs.com/):** Leitura e parser de arquivos `.xlsx` no navegador do cliente.
- **[Chart.js](https://www.chartjs.org/):** Renderização de gráficos vetoriais em Canvas.
- **SVG Dinâmico:** Geometria da planta de implantação com coordenadas amarradas à Linha de Balanço.

---

## 🚀 Como Publicar no GitHub Pages

Para disponibilizar o link público de acesso para a equipe de obra e diretoria:

1. Crie um repositório no seu GitHub (exemplo: `dashboard-obra-sao-luis`).
2. Faça o upload do arquivo `index.html` na raiz do repositório (`main` ou `master`).
3. Adicione este arquivo `README.md`.
4. No repositório, acesse a aba **Settings** > menu lateral **Pages**.
5. Em **Build and deployment**:
   - **Source:** *Deploy from a branch*.
   - **Branch:** selecione `main` (ou `master`) e a pasta `/ (root)`.
   - Clique em **Save**.
6. Aguarde cerca de 1 a 2 minutos. O GitHub gerará o link seguro de produção:
   ```
   https://<seu-usuario>.github.io/dashboard-obra-sao-luis/
   ```

---

## 🔄 Rotina de Atualização Periódica

Para atualizar o dashboard com as medições semanais da obra:

1. Acesse o **Prevision** e exporte a planilha de acompanhamento no formato **Excel (.xlsx)**.
2. Abra o dashboard no navegador pelo link do GitHub Pages.
3. Clique no botão **"Subir Planilha Prevision (.xlsx)"** no cabeçalho superior.
4. Selecione o arquivo exportado. O motor de dados processará os novos percentuais e datas instantaneamente, atualizando o mapa e os gráficos.

---

## 📂 Estrutura de Arquivos

```text
├── index.html       # Aplicação completa (HTML, estilos, SVG do mapa, scripts e base pré-carregada)
└── README.md        # Documentação técnica e operacional do projeto
```

---

*Desenvolvido para Gestão Visual e Controle de Prazos em Engenharia Civil.*