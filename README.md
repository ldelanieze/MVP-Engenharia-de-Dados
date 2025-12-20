# MVP: Engenharia de Dados - Análise Global do Futebol Feminino

## 1. Objetivo
O problema central abordado neste MVP é a carência de uma análise comparativa estruturada sobre o perfil físico, a disparidade econômica e o fluxo de talentos no futebol feminino global. O projeto consistiu na construção de um pipeline de dados automatizado (ETL) no Google Colab para transformar dados brutos em um **Esquema Estrela (Star Schema)**, permitindo análises granulares sobre o mercado da modalidade.

**Perguntas Respondidas:**
* **P1/P1.2 - Disparidade de Valor:** Análise da concentração de capital nas ligas de elite comparadas ao mercado global.
* **P2/P2.1 - Perfil Físico e Lateralidade:** Diferenças de altura, idade e preferência de pé dominante por posição tática.
* **P3 - Exportação de Talentos:** Identificação dos principais polos provedores de atletas.
* **P4 - Longevidade Profissional:** Análise do tempo de atividade profissional por função tática.

---

## 2. Catálogo de Dados (Data Dictionary)

| Tabela | Atributo | Descrição Detalhada | Domínio (Tipo) | Valores Mín/Máx Esperados |
| :--- | :--- | :--- | :--- | :--- |
| **Dim_Jogadora** | `soccer_id` | Identificador único da jogadora (Chave Primária). | Inteiro (PK) | N/A |
| **Dim_Jogadora** | `player_name` | Nome completo da atleta. | String | N/A |
| **Dim_Jogadora** | `height` | Altura em centímetros (pós-imputação). | Float | 140.0 a 210.0 |
| **Dim_Jogadora** | `foot` | Lateralidade / Pé dominante. | Categórico | left, right, both |
| **Dim_Jogadora** | `position_class` | Classe simplificada da posição tática. | Categórico | Attacker, Midfielder, Defender, Goalkeeper |
| **Dim_Clube** | `current_club_id` | Identificador único do clube. | Inteiro (PK) | N/A |
| **Fato_Perfil** | `age` | Idade da jogadora (calculada via ETL). | Inteiro | 14 a 45 |
| **Fato_Perfil** | `market_value` | Valor de mercado estimado em Euros (€). | Float | 0.0 a 1.500.000+ |
| **Fato_Perfil** | `citizenship1` | Nacionalidade principal da atleta. | Categórico | Países |

---

## 3. Arquitetura e Tecnologias
* **Linguagem:** Python 3.10+
* **Bibliotecas:** Pandas, Seaborn, Matplotlib, Numpy.
* **Arquitetura:** Pipeline de medalhão (Raw, Silver, Gold) com modelagem multidimensional.
* **Infraestrutura:** Google Colab integrado ao Google Drive (Data Lake Cloud).

---

## 4. Evidências de Execução e Resultados
Nesta seção, apresentamos as evidências das respostas às perguntas do MVP.

### 4.1 Disparidade Econômica (P1.2)
![Disparidade de Valor](Evidencia%201.2.PNG)
**Discussão Técnica:** A análise confirma a disparidade extrema entre a elite e o mercado global. A **Primera División Femenina** lidera com média de **€ 58.806**, enquanto a média das demais ligas cai para apenas **€ 1.596**. Essa diferença de **37 vezes** prova a concentração de capital nos polos de destaque.

### 4.2 Preferência de Pé Dominante (P2.1)
![Lateralidade](Evidencia%202.1.PNG)
**Discussão Técnica:** O pé direito predomina, mas há maior presença de canhotas e ambidextras no ataque e meio-campo, onde a versatilidade motora favorece a criação de jogadas.

### 4.3 Longevidade Profissional (P4)
![Mapa de Calor](Evidencia%204.PNG)
**Discussão Técnica:** O mapa de calor revela que a posição de Goleira (Goalkeeper) apresenta maior retenção em faixas etárias avançadas (31-35 e 35+), indicando maior longevidade física na função.

### 4.4 Evidência de Execução do Pipeline
![Execução do Pipeline](Evidencia%20Pipeline.PNG)

**Discussão Técnica:** Esta evidência demonstra o sucesso da automação do pipeline ETL. O log confirma a extração dos dados brutos, o processamento das transformações na camada Silver e a persistência final dos dados modelados (Star Schema) na camada Gold. A presença dos arquivos `.csv` gerados no diretório de destino comprova que o pipeline é capaz de sustentar de forma autônoma o ciclo de vida dos dados, desde a ingestão até o armazenamento para análise.

---

## 5. Autoavaliação

### Atingimento de Objetivos
O projeto entregou um pipeline funcional que mitigou inconsistências severas do dataset original. Validamos que a centralização econômica na Europa molda a valorização e a retenção de talentos mundiais.

### Superação de Desafios Técnicos
* **Qualidade dos Dados:** Diferente do projeto anterior, este MVP tratou 18.69% de nulos em idade e lacunas em altura, atingindo **0% de nulos** em atributos críticos.
* **Automação:** O pipeline é 100% automatizado, garantindo reprodutibilidade via Google Drive sem necessidade de uploads manuais.
* **Organização:** Código limpo, sem redundâncias e com tratamento preventivo de erros de variáveis.

### Trabalhos Futuros
1. Migração do pipeline para Spark/Databricks para lidar com Big Data.
2. Integração com Power BI para dashboards dinâmicos.
