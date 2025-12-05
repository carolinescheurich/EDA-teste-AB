# 🧪 Análise de Funil e Teste A/B com Sistema de Recomendação

## Contexto do Projeto
Este projeto realiza uma Análise Exploratória de Dados (EDA) combinada com Teste A/B, com o objetivo de avaliar o impacto de um novo sistema de recomendação dentro do aplicativo de e-commerce.  

A hipótese do time de produto era que o sistema melhorado aumentaria o interesse dos usuários por produtos e, consequentemente, a taxa de conversão ao longo do funil de vendas.

## 🎯 Objetivos da Análise
1. Investigar o comportamento dos usuários nos grupos de teste (A e B).  
2. Avaliar o fluxo dos usuários no funil: **login → product_page → product_cart → purchase**.  
3. Realizar teste estatístico para identificar impacto do experimento na conversão.  
4. Apoiar a decisão de continuidade ou rollback da nova funcionalidade.

## 🧩 Estrutura do Funil de Eventos

| Evento | Descrição |
|--------|-----------|
| `login` | Acesso ao aplicativo |
| `product_page` | Visualização de produtos |
| `product_cart` | Produto adicionado ao carrinho |
| `purchase` | Compra concluída |

Essas etapas representam o caminho principal até a conversão final.

## ⚙️ Metodologia

### 1. **Preparação e filtragem dos dados**
- Seleção do período representativo do experimento  
- Limpeza e padronização das colunas  
- Conversão de datas e criação de indicadores de presença nos eventos  

### 2. **Construção do Funil**
- Identificação do primeiro timestamp de cada evento por usuário  
- Criação de flags binárias (0/1) para cada etapa  
- Cálculo de conversões por grupo e por estágio  

### 3. **Teste A/B**
- Comparação entre grupos:  
  - **A** → controle  
  - **B** → sistema de recomendação
- Hipóteses:
  - H₀: não há diferença entre as taxas de conversão dos grupos  
  - H₁: existe diferença significativa  
- Teste estatístico: `proportions_ztest` (α = 5%)  
- Cálculo de lift e interpretação de resultados  

## 📈 Principais Insights e Conclusões

| Etapa | Grupo A | Grupo B | Resultado |
|------|---------|---------|----------|
| Login | 100% | 99,89% | Sem diferença significativa |
| Product Page | 64,71% | 56,21% | **Queda significativa (p < 0.001)** |
| Product Cart | ↓ | ↓ | Grupo B sempre pior |
| Purchase | ↓ | ↓ | Conversão final reduzida no grupo B |

🔎 **Ponto crítico do funil:**  
Uma queda expressiva ocorre entre **login → product_page** para o grupo B, reduzindo o interesse do usuário por produtos logo no início da jornada.

---

### 🧾 Decisão Final

**O novo sistema de recomendação NÃO deve ser implementado**  
Motivos:
- Conversões **pioraram em todas as etapas do funil**
- Diferença estatisticamente significativa em pontos-chave
- Meta do experimento **não atingida**

📌 **Próximos Passos Recomendados**
- Revisar lógica do sistema de recomendação  
- Realizar testes com segmentações menores  
- Aplicar prototipação e pesquisas qualitativas antes de novo rollout  

## 🛠️ Tecnologias e Bibliotecas Utilizadas
O projeto foi desenvolvido em **Python**, utilizando as bibliotecas:

- **Pandas** → manipulação de dados  
- **NumPy** → operações numéricas  
- **Matplotlib** e **Seaborn** → visualizações  
- **Statsmodels** → testes estatísticos  
- **Jupyter Notebook** → análise e documentação 
