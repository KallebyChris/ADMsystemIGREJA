# ⛪ Sistema de Gerenciamento Administrativo e Ministerial da Igreja

> **Projeto:** Banco de Dados Relacional (SQL)  
> **Autor:** Kalleby Christian Lima das Graças  
> **RGM:** 45132089  
> **Versão:** 1.1

---

## 📋 Sobre o Projeto

Este projeto consiste na modelagem e implementação de um banco de dados relacional para gerenciar as informações centrais de uma igreja local. O objetivo é integrar dados administrativos e ministeriais, garantindo a integridade e organização das informações.

[cite_start]O sistema foi projetado para atender ao **Mini-mundo** descrito na documentação, abrangendo o controle de membros, cultos, ministérios, eventos, ofertas, visitantes e atendimentos pastorais[cite: 8, 9, 78, 79].

## 🛠 Tecnologias Utilizadas

* **Linguagem:** SQL (Structured Query Language)
* **Modelagem:** Conceitual (DER) e Lógico
* [cite_start]**Normalização:** Aplicada até a 3ª Forma Normal (3FN) [cite: 138]
* **SGBD Sugerido:** MySQL Workbench ou PostgreSQL (PGAdmin)

---

## 🗂 Estrutura do Banco de Dados

O banco de dados foi estruturado respeitando as regras de integridade referencial e atomicidade. As principais entidades mapeadas são:

### Tabelas Principais (Entidades Fortes)
* [cite_start]**Membro:** Dados pessoais, contato e status eclesiástico[cite: 11, 124].
* [cite_start]**Ministério:** Grupos de atuação (Ex: Louvor, Infantil)[cite: 129].
* [cite_start]**Local:** Templos, salas e auditórios com capacidade definida[cite: 14, 135].
* [cite_start]**Pregador & Sermão:** Registro histórico das mensagens ministradas[cite: 12, 133].

### Tabelas Transacionais e Associativas
* [cite_start]**Culto:** Centraliza a liturgia, vinculando local, pregador, sermão e estatísticas[cite: 12, 133].
* [cite_start]**Oferta:** Registro financeiro vinculado a um culto específico[cite: 13, 134].
* [cite_start]**Participação_Ministério:** Tabela associativa (N:N) que vincula membros a ministérios e suas funções[cite: 24, 227].
* **Escala:** Gerenciamento de voluntários em datas específicas[cite: 15, 229].

---

## 🚀 Scripts SQL Disponíveis

Neste repositório, você encontrará os seguintes scripts para execução:

1.  **DDL (Data Definition Language):** Comandos `CREATE TABLE` para estruturar o banco e definir chaves primárias (PK) e estrangeiras (FK).
2.  **DML (Data Manipulation Language):**
    * `INSERT`: Povoamento inicial com dados fictícios para testes.
    * `SELECT`: Consultas simples e complexas (com `JOIN`, `GROUP BY`, `ORDER BY`).
    * `UPDATE` e `DELETE`: Exemplos de manutenção de dados.

### Exemplo de Consulta (View Preview)
*Verificando a escala de voluntários:*

```sql
SELECT 
    m.nome AS Nome_Membro, 
    min.nome AS Ministerio, 
    esc.data AS Data_Escala,
    esc.funcao AS Funcao
FROM Escala esc
INNER JOIN Membro m ON esc.id_membro = m.id_membro
INNER JOIN Ministerio min ON esc.id_ministerio = min.id_ministerio
ORDER BY esc.data DESC;
