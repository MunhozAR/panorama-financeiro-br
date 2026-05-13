# Metodologia e Decisões Analíticas

## Fonte de dados
- **IF.data / Banco Central do Brasil**
- Seção "Dados a partir de 2025": trimestres 2025T1 a 2025T4
- Seção "Dados de 2000 a 2024": trimestres 2024T1 a 2024T4
- Tipo de instituição: Conglomerados Financeiros e Instituições Independentes
- Relatório: Resumo

## Decisões analíticas

### 1. Banco Inter — múltiplas razões sociais
O Banco Inter aparece como `INTERMEDIUM` nos trimestres mais antigos
e como `INTER` nos mais recentes, refletindo a mudança de razão social
ocorrida em 2018. Ambas as entradas foram consolidadas sob o nome
comercial `Inter` para permitir análise temporal contínua.

### 2. Mercado Pago — duas entidades regulatórias
O Mercado Pago opera com duas entidades distintas no IF.data:
- `MERCADO PAGO INSTITUIÇÃO DE PAGAMENTO LTDA.` (entidade de pagamento)
- `MERCADO PAGO IP - FINANCEIRO` (entidade financeira, criada em 2025T4)

Decisão: manter as duas entidades separadas para preservar a riqueza
analítica e refletir a expansão regulatória da empresa.

### 3. ROE anualizado
O Lucro Líquido reportado no IF.data é trimestral.
Fórmula utilizada: `ROE_anualizado = (Lucro Líquido / Patrimônio Líquido) × 4`

### 4. Valores monetários
Os CSVs do IF.data utilizam ponto como separador de milhar (formato BR).
Conversão realizada via `str.replace('.', '')` antes do cast para float.
Todos os valores estão em R$ mil conforme padrão do IF.data.

## Limitações conhecidas

### Carteira de Crédito — dados incompletos em 2024
Os trimestres de 2024 (2024T1 a 2024T4) retornam NaN para a coluna
"Carteira de Crédito". A causa provável é divergência de nomenclatura
entre as duas seções do IF.data (2024 vs 2025+).

**Impacto:** análises de Carteira de Crédito limitadas a 2025T1-2025T4.
**Métricas não afetadas:** ROE, Ativo Total, Lucro Líquido, Patrimônio Líquido.

**Sugestão para versão futura:** mapear nomes alternativos da coluna
nos CSVs de 2024 e ajustar o script de consolidação.

## Período analisado
8 trimestres: 2024T1 a 2025T4 (2 anos completos)

## Instituições analisadas
| Banco | Categoria | Trimestres disponíveis |
|---|---|---|
| Itaú | Tradicional | 8 |
| Bradesco | Tradicional | 8 |
| Banco do Brasil | Tradicional | 8 |
| Santander | Tradicional | 8 |
| Nubank | Digital | 8 |
| C6 Bank | Digital | 8 |
| Inter | Digital | 8 |
| PagBank | Fintech Pagamento | 8 |
| Mercado Pago (Pagamento) | Fintech Pagamento | 8 |
| Mercado Pago (Financeiro) | Fintech Pagamento | 1 |
| PicPay | Fintech Pagamento | 5 |
