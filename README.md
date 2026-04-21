Objetivo:  Criar o diagrama dimensional – star schema – com base no diagrama relacional disponibilizado.

# Projeto: Modelagem Dimensional - Esquema em Estrela (Star Schema)

## 📌 Descrição do Projeto
Este repositório contém a resolução de um desafio prático de modelagem de dados para Data Warehouse. O objetivo principal foi transformar um modelo de banco de dados relacional (focado no sistema de uma universidade) em um **Diagrama Dimensional (Star Schema)**, otimizado para consultas analíticas e regras de negócios específicas.

## 🎯 Objetivo de Análise
O escopo do projeto exigiu uma mudança de perspectiva arquitetural:
- **Foco da Análise:** O `Professor`.
- **Métricas:** Dados sobre os docentes, disciplinas lecionadas, cursos vinculados e departamentos.
- **Restrição:** Exclusão intencional de dados transacionais referentes aos `Alunos` e `Matrículas`, isolando o contexto de atuação do corpo docente.

## 🏗️ Arquitetura do Modelo (Star Schema)

Para atender aos requisitos analíticos, a modelagem foi estruturada da seguinte forma:

### 1. Definição da Granularidade
A Tabela Fato foi modelada no nível de **oferta de disciplina**: Uma linha representa cada disciplina ofertada por um professor, para um curso específico, em uma determinada data.

### 2. Tabelas Dimensão
As dimensões foram criadas para fornecer o contexto descritivo das métricas. Para garantir boas práticas de Data Warehouse, chaves artificiais (Surrogate Keys) são recomendadas.

* **`Dim_Professor`**: Atributos exclusivos do docente (ID, Nome, Titulação).
* **`Dim_Departamento`**: Informações da unidade acadêmica à qual o professor está vinculado, incluindo o coordenador responsável.
* **`Dim_Curso`**: Dados dos cursos que recebem a oferta das disciplinas.
* **`Dim_Disciplina`**: Detalhamento das matérias ministradas (código, nome, carga horária teórica).
* **`Dim_Data`**: Dimensão de tempo adicionada estrategicamente para compensar a ausência de histórico no modelo relacional original. Permite análises sazonais (ano, semestre, trimestre de oferta).

### 3. Tabela Fato
A Tabela Fato atua como o centro do modelo em estrela, unificando o contexto acadêmico.

* **`Fato_Atuacao_Professor`**: 
    * **Chaves Estrangeiras (FKs):** `fk_professor`, `fk_departamento`, `fk_curso`, `fk_disciplina`, `fk_data_oferta`.
    * **Métricas Aditivas:** `qtd_disciplinas` (fator de contagem de alocação) e `carga_horaria_lecionada` (esforço do professor no período).

## 📊 Representação Visual

*(Adicione aqui a imagem do seu modelo dimensional criado em uma ferramenta de diagramação, como o MySQL Workbench, draw.io ou similar)*

```text
[ Diagrama Star Schema .png / .jpg ]

```

## 🛠️ Tecnologias e Conceitos Aplicados

- Modelagem de Banco de Dados Relacional (OLTP)
- Modelagem Dimensional (OLAP)
- Estruturação de Star Schema
- Definição de Granularidade e Tabelas Fato/Dimensão
- Design de Data Warehouse
---
Projeto desenvolvido como parte de desafio prático de arquitetura de dados.
