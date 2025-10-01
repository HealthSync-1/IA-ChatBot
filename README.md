# HealthSync / IMREA — Artificial Intelligence & Chatbot  
## Bases de dados sintéticas para treinamento de modelos (Teleconsulta & Adoção de Tecnologia)

> Este repositório contém **duas bases de dados sintéticas** (sem PII) para apoiar o treinamento de modelos de IA/Chatbot no contexto do **IMREA / Teleconsulta**. Os dados foram gerados com regras de domínio e ruído controlado para simular cenários realistas, preservando privacidade.

---

## 1) Objetivo do trabalho

- **Levantar e entregar** uma base de dados (ou mais) **aderente ao tema** do desafio (saúde / teleconsulta / adoção de tecnologia).
- **Explicar os dados** (como foram criados/coletados, o que significam, tamanho/qualidade, variáveis importantes, **rótulos**, e **qual tarefa de IA** pretendemos realizar).
- **Entregar**:
  - Um **.zip** com os dados (nossos arquivos `.csv`)  
  - Um **.txt** com as explicações e nomes dos membros do grupo.

---

## 2) O que fizemos (resumo)

1. **Definimos dois recortes de dados** totalmente **sintéticos**:
   - **Dataset 1:** Dificuldade de pessoas **55+** em adotar tecnologia (barreiras e nível de dificuldade).
   - **Dataset 2:** Uso de **tecnologia na saúde** (Teleconsulta, Portal do Paciente/EHR, Wearables), engajamento e indicador de uso de alto valor.

2. **Geramos os dados sintéticos** com distribuições plausíveis (normal, Poisson, categóricas com probabilidades) e **regras de domínio** para manter coerência (ex.: maior letramento digital → menor dificuldade; maior adesão → maior engajamento).

3. **Documentamos tudo** no arquivo `EXPLICACOES_E_EQUIPE.txt` (fonte, significado das colunas, rótulos, tamanho, qualidade, objetivos de IA, ética/LGPD).

4. **Empacotamos** os `.csv` + `.txt` em um **.zip** pronto para envio.

---

## 3) Por que os dados aderem ao tema (+50)

- **Teleconsulta IMREA / Saúde:**  
  - Dataset 1 foca **barreiras digitais** (acesso, letramento, autoeficácia, limitações sensoriais/motoras) — variáveis que **impactam diretamente** a capacidade do paciente de participar de teleconsultas.
  - Dataset 2 foca **tecnologias de saúde** (Teleconsulta, EHR Portal, Wearables), **engajamento** e **uso de alto valor** — indicadores que ajudam a priorizar intervenções e personalizar o suporte do Chatbot.

- **Aplicação prática no Chatbot/IA:**  
  - Prever perfis com maior **dificuldade digital** (onboarding sob medida).  
  - Estimar probabilidade de **uso de alto valor** e **engajamento** (intervenções e lembretes direcionados).

---

## 4) Entregáveis

- **datasets_healthsync_ai.zip**  
  Contém:
  - `dataset_1_older_adults_tech_difficulty.csv`
  - `dataset_2_health_technology_usage.csv`
  - `EXPLICACOES_E_EQUIPE.txt` (explicações completas + membros)

> Observação: Os arquivos são CSV com cabeçalho (UTF-8), prontos para uso em Excel, Python (pandas), R etc.

---

## 5) Estrutura de pastas (sugestão)

```
.
├─ datasets_healthsync_ai.zip
├─ dataset_1_older_adults_tech_difficulty.csv
├─ dataset_2_health_technology_usage.csv
├─ EXPLICACOES_E_EQUIPE.txt
└─ README.md  ← este arquivo
```

> Caso a plataforma exija apenas o `.zip`, garanta que **ele** contenha os dois `.csv` + o `.txt`.

---

## 6) Descrição dos dados (+50)

### 6.1 Dataset 1 — Older Adults Tech Difficulty (600 linhas)
**Objetivo:** identificar **níveis de dificuldade** na adoção de tecnologia por pessoas **55+** para orientar onboarding e suporte na teleconsulta.

**Principais colunas (amostra):**
- **Demografia & acesso:**  
  `age` (55–89), `gender` (F/M/Outro), `education` (Fundamental… Pós), `region` (Norte… Rural), `household_income` (faixas),  
  `internet_access` (0/1), `device_ownership` (Nenhum/Feature/Smartphone/Smartphone+PC/Tablet), `years_using_smartphone` (0–20).
- **Habilidades & atitudes:**  
  `digital_literacy` (0–100), `self_efficacy` (0–100), `privacy_concern` (0–100).
- **Limitações:**  
  `vision_impairment`, `hearing_impairment`, `motor_impairment` (0/1).
- **Uso & experiência prévia:**  
  `weekly_smartphone_use_hours` (0–50), `uses_messaging_apps` (0/1), `uses_video_calls` (0/1), `uses_banking_apps` (0/1), `uses_telehealth_before` (0/1).
- **Alvos (rótulos):**  
  `difficulty_score` (0–100, contínuo) e **`difficulty_level`** {Baixa, Média, Alta}.

**Tarefas de IA sugeridas:**
- **Classificação:** prever `difficulty_level`.  
- **Regressão:** prever `difficulty_score`.  
- **Clustering:** segmentar perfis para estratégias de suporte.

---

### 6.2 Dataset 2 — Health Technology Usage (700 linhas)
**Objetivo:** modelar **engajamento** com tecnologia na saúde e o rótulo **`HighValueUse`** (uso de alto valor).

**Principais colunas (amostra):**
- **Perfil & modalidade:**  
  `patient_age` (18–89), `has_chronic_condition` (0/1), `region`, `provider_type` (Clínico Geral, Fisio, etc.),  
  `tech_modality` {Teleconsulta, EHR Portal, Wearable}.
- **Comportamento & percepção:**  
  `sessions_last_90d` (0–40), `adherence_rate` (0–1), `satisfaction_0_100` (0–100).
- **Proxies clínicos & escore composto:**  
  `baseline_er_visits`, `post_er_visits` (0–6), `bp_control_improved` (0/1),  
  `engagement_score` (0–100, contínuo).
- **Alvo (rótulo):**  
  **`HighValueUse`** (0/1).

**Tarefas de IA sugeridas:**
- **Classificação binária:** `HighValueUse`.  
- **Regressão:** `engagement_score`.  
- **Análises descritivas:** comparar `baseline_er_visits` vs `post_er_visits` por grupos.

---

## 7) Qualidade, limitações e ética

- Dados **100% sintéticos** (sem PII), com **coerência interna** via regras de domínio.  
- **Sem vazios** por construção; variância suficiente para treinos básicos.  
- **Limitação:** proxies clínicos e relações não devem ser interpretados como **causalidade real**.  
- **Ética/LGPD:** para dados reais no futuro, aplicar consentimento, minimização, finalidade e segurança.

---

## 8) Como usar os dados (exemplos)

### Python (pandas)
```python
import pandas as pd

df1 = pd.read_csv("dataset_1_older_adults_tech_difficulty.csv")
df2 = pd.read_csv("dataset_2_health_technology_usage.csv")

print(df1.shape, df2.shape)
print(df1.dtypes)
print(df2.dtypes)
```

### Exemplos de modelagem
- **Classificação (ex.: LogisticRegression/Tree)** para `difficulty_level` e `HighValueUse`.  
- **Regressão (ex.: LinearRegression/GBR)** para `difficulty_score` e `engagement_score`.  
- **Segmentação (ex.: KMeans)** para perfis de suporte/engajamento.

> Boas práticas: treino/validação/teste, validação cruzada, métricas (Accuracy/F1/AUC para classificação; MAE/RMSE para regressão).

---

## 9) Checklist de conformidade com a entrega

- [x] **Dados aderentes ao tema** (teleconsulta/saúde/adoção tecnológica).  
- [x] **Explicações detalhadas** no `.txt` (fonte/como gerado, significado, tamanho/qualidade, variáveis importantes, **rótulos** e **objetivos de IA**).  
- [x] **Entrega em `.zip`** contendo os dois `.csv` + `.txt`.  
- [x] **Sem PII**, dados sintéticos.  
- [x] **Nomes/RMs** dos integrantes no `.txt`.

### Penalidades (atenção)
- Entrega **fora do prazo**: −100.  
- **Arquivos errados ou corrompidos**: perde a pontuação do item faltante.  
> Recomendação: validar a abertura dos CSVs antes de enviar e conferir o conteúdo do `.zip`.

---

## 10) Membros do grupo

- **Maicon** — RM **561279** — Turma **1TDSPW**  
- **Richard** — RM **566127** — Turma **1TDSPW**  
- **Laura** — RM **566376** — Turma **1TDSPW**

> Edite esta seção caso precise atualizar nomes e RMs.

---

## 11) Guia rápido para o avaliador

- Abra `EXPLICACOES_E_EQUIPE.txt` para a **narrativa completa**.  
- Os **rótulos** a serem previstos estão claros: `difficulty_level` (Dataset 1) e `HighValueUse` (Dataset 2).  
- Os **CSV** carregam em Excel/Sheets e em notebooks (pandas/R).  
- O **.zip** inclui **todos** os arquivos requeridos.

---

## 12) Licença & uso

- Bases **sintéticas** disponibilizadas para **P&D/ensino** no contexto deste desafio.  
- Ao trabalhar com **dados reais** no futuro: cumprir **LGPD** (consentimento, minimização, segurança, finalidade e transparência).

---

**Fim.**
