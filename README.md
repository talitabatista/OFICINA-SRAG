---
title: "CADERNO DE ANÁLISES DE SRAG"
output: html_document
---

# Introdução 

  O caderno de análises de Síndrome Respiratória Aguda Grave (SRAG) é um documento que compila análises epidemiológicas de dados relacionados a SRAG extraídos do SIVEP-Gripe.

  O R é um ambiente de software livre altamente utilizado para análises estatísticas e gráficas. Sua aplicação em análises de dados em saúde é amplamente reconhecida devido às suas poderosas capacidades de manipulação de dados, análise estatística e visualização. No contexto das análises de SRAG, o R é utilizado para a manipulação de Dados, utilizando de pacotes como dplyr, data.table e tidyverse para limpar, transformar e preparar grandes volumes de dados de saúde para análise; implementação de técnicas estatísticas avançadas utilizando pacotes como stats, psych e survival para identificar padrões e realizar inferências a partir dos dados de SRAG; visualização de dados, por meio da criação de gráficos e mapas informativos utilizando pacotes como ggplot2, plotly e leaflet, facilitando a comunicação dos resultados das análises para diferentes públicos.
  
  
### Passo 1: Baixar e Instalar o R

1. **Download do R**:
   - Acesse o site oficial do R: [CRAN R Project](https://cran.r-project.org/).
   - Clique no link "Download R for Windows" (ou "Download R for macOS" ou "Download R for Linux" se você estiver utilizando um desses sistemas operacionais).
   - Siga as instruções para baixar o instalador adequado para o seu sistema operacional.

2. **Instalação do R**:
   - Após baixar o instalador, execute-o.
   - Siga as instruções na tela para completar a instalação.
   - Durante a instalação, você pode aceitar as configurações padrão recomendadas.

### Passo 2: Instalar o RStudio 

RStudio é um ambiente de desenvolvimento integrado (IDE) que facilita o uso do R.

1. **Download do RStudio**:
   - Acesse o site do RStudio: [RStudio](https://www.rstudio.com/products/rstudio/download/).
   - Baixe a versão gratuita do RStudio Desktop.

2. **Instalação do RStudio**:
   - Execute o instalador baixado.
   - Siga as instruções para completar a instalação.

### Passo 3: Instalar Pacotes Necessários

Abra o R ou o RStudio e utilize o seguinte código para instalar os pacotes necessários. Para garantir que os pacotes sejam carregados corretamente, vamos usar a função `install.packages` para instalar e `library` para carregar os pacotes.

```
# Lista de pacotes para instalar
pacotes <- c(
  "data.table",    # Pacote para manipulação eficiente de grandes conjuntos de dados
  "openxlsx",      # Leitura e escrita de arquivos Excel
  "dttr2",         # Ferramentas para manipulação e transformação de dados temporais
  "foreign",       # Leitura de dados armazenados em outros formatos (DBF, SPSS, Stata, SAS)
  "tidyverse",     # Conjunto de pacotes para ciência de dados
  "lubridate",     # Facilita o trabalho com datas e horas
  "reshape2",      # Ferramentas para remodelar dados
  "haven",         # Importação e exportação de dados em formatos SAS, Stata e SPSS
  "vctrs",         # Base para vetores e tipagem em R
  "readr",         # Leitura rápida de dados retangulares (CSV)
  "utils",         # Funcionalidades utilitárias diversas
  "sqldf",         # Executa consultas SQL em data frames
  "stringr",       # Facilita a manipulação de strings
  "dplyr",         # Ferramentas para manipulação de dados
  "psych",         # Ferramentas para análise psicométrica
  "skimr",         # Sumários estatísticos de conjuntos de dados
  "kableExtra",    # Melhorias para a função kable do knitr
  "plotly",        # Criação de gráficos interativos
  "magrittr",      # Fornece o operador pipe (%>%) para encadeamento de operações
  "knitr",         # Integração de código R em documentos LaTeX, HTML e Markdown
  "readxl",        # Leitura de arquivos Excel
  "htmlTable",     # Ferramentas para criar e formatar tabelas HTML
  "zoo",           # Manipulação de séries temporais
  "ggthemes",      # Temas adicionais para ggplot2
  "scales",        # Ferramentas para dimensionar e formatar dados em ggplot2
  "ggrepel",       # Adiciona rótulos aos gráficos ggplot2 sem sobreposição
  "sf",            # Manipulação de dados espaciais simples
  "rnaturalearth", # Download e visualização de dados naturais da Terra
  "rnaturalearthdata", # Conjunto de dados naturais da Terra
  "ggspatial",     # Ferramentas para criar mapas e adicionar elementos espaciais ao ggplot2
  "geobr",         # Conjunto de dados geográficos do Brasil
  "viridis"        # Mapas de cores para visualização de dados
)

# Instalar pacotes que ainda não estão instalados
novos_pacotes <- pacotes[!(pacotes %in% installed.packages()[,"Package"])]
if(length(novos_pacotes)) install.packages(novos_pacotes)

# Carregar todos os pacotes
lapply(pacotes, require, character.only = TRUE)

```



# Definir Diretório de Trabalho onde os arquivos serão salvos e carregados.

<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">


getwd() # Verificar o diretório de trabalho atual


setwd("C:/Users/talita.batista/Documents/TrabalhosGTGripe/OFICINA_SRAG/OFICINA_SRAG") # Definir o diretório de trabalho


list.files() # Listar os arquivos presentes no diretório definido

</code></pre>
</div>


# Carregar Dados DBF

<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">


SRAG <- #seu caminho


</code></pre>
</div>

# Remover Duplicidades

  1.  Identificar registros duplicados com base em múltiplas colunas
  
  2.  Selecionar o registro com menos valores ausentes para cada grupo de duplicados
  
  3.  Encontrar registros únicos (não duplicados)
  
  4.  Combinar registros duplicados selecionados e registros não duplicados


<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">

duplicados <- SRAG %>%
  group_by(NM_PACIENT, NU_CPF, DT_NASC, CS_SEXO, NM_MAE_PAC, DT_SIN_PRI) %>%
  filter(n() > 1) %>%
  ungroup()


registros_duplicados <- duplicados %>%
  group_by(NM_PACIENT, NU_CPF, DT_NASC, CS_SEXO, NM_MAE_PAC, DT_SIN_PRI) %>%
  mutate(num_na = rowSums(is.na(across(everything())))) %>%
  arrange(num_na) %>%
  slice(1) %>%
  ungroup() %>%
  select(-num_na)


registros_nao_duplicados <- SRAG %>%
  filter(!duplicated(SRAG %>% select(NM_PACIENT, NU_CPF, DT_NASC, CS_SEXO, NM_MAE_PAC, DT_SIN_PRI)))


SRAG_final <- bind_rows(registros_duplicados, registros_nao_duplicados)

</code></pre>
</div>

# Processamento Inicial dos Dados. Conversão de tipos de dados e a criação de novas colunas

  1.  Removendo inconsistência: Aplicação da definição de caso
  2.  Transformação e criação de colunas
  

<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">

SRAG_final <- SRAG_final %>% 
  mutate(SEM_PRI = as.numeric(SEM_PRI)) %>%
  mutate(variavel01 = ifelse(HOSPITAL == 1 | EVOLUCAO == 2, 1, 0),
         variavel02 = ifelse(TOSSE == 1 | GARGANTA == 1, 1, 0),
         variavel03 = ifelse(DISPNEIA == 1 | SATURACAO == 1 | DESC_RESP == 1, 1, 0)) %>% 
  mutate(caso_srag = ifelse(variavel01 == 1 & variavel02 == 1 & variavel03 == 1, 1,0))


SRAG_final <- SRAG_final %>%  
  mutate(PCR_SARS2 = as.numeric(as.character(PCR_SARS2)), 
         AN_SARS2 = as.numeric(as.character(AN_SARS2)), 
         CLASSI_FIN = as.numeric(as.character(CLASSI_FIN)), 
         CRITERIO = as.numeric(as.character(CRITERIO)), 
         DT_SIN_PRI = dmy(DT_SIN_PRI), 
         DT_EVOLUCA = dmy(DT_EVOLUCA)) %>%  
  mutate(ANO = case_when(
    DT_SIN_PRI >= ymd("2019-12-29") & DT_SIN_PRI < ymd("2021-01-03") ~ "2020", 
    DT_SIN_PRI >= ymd("2021-01-03") & DT_SIN_PRI < ymd("2022-01-02") ~ "2021", 
    DT_SIN_PRI >= ymd("2022-01-02") & DT_SIN_PRI < ymd("2023-01-01") ~ "2022", 
    DT_SIN_PRI >= ymd("2023-01-01") & DT_SIN_PRI < ymd("2023-12-31") ~ "2023", 
    DT_SIN_PRI >= ymd("2023-12-31") & DT_SIN_PRI < ymd("2024-12-29") ~ "2024")) %>% 
  mutate(ANO_SEM_PRI = paste(ANO, SEM_PRI, sep = "_")) %>% 
  mutate(mes_pri_sint1 = ifelse(month(DT_SIN_PRI) %in% 1:9, paste0("0", month(DT_SIN_PRI)), as.character(month(DT_SIN_PRI)))) %>% 
  mutate(mes_pri_sint = paste0(year(DT_SIN_PRI), "_", mes_pri_sint1)) %>% 
  mutate(teste_covid = ifelse(PCR_SARS2 == 1 | AN_SARS2 == 1, 1, 0)) %>%         # Cria uma nova variável teste_covid que indica se o paciente teve um teste                                                                                                             positivo para COVID-19, baseado em PCR ou teste de antígeno.
  mutate(classi_nova = ifelse(CLASSI_FIN == 5 & teste_covid == 1, 5, 0)) %>%           # Cria uma nova variável classi_nova onde os casos confirmados de COVID-19                                                                                                                                                                           (CLASSI_FIN == 5 e teste_covid == 1) recebem o valor 5, e os outros recebem 0.
  mutate(classi_nova = ifelse(is.na(classi_nova) | classi_nova == 0, CLASSI_FIN, classi_nova)) %>%  # Atualiza classi_nova para ser igual a CLASSI_FIN se classi_nova for NA ou 0, mantendo os valores já atribuídos como 5.
  mutate(classi_teste = ifelse(is.na(classi_nova), 0, classi_nova)) %>%   #Cria uma nova variável classi_teste onde 'classi_nova' é substituída por 0 se for NA, caso contrário, mantém o valor de classi_nova.

  mutate(variavel1 = ifelse(classi_teste == 5 & DT_SIN_PRI > ymd("2020-02-15"), 0, 1)) %>%    # Cria uma nova variável 'variavel1' que indica casos de COVID-19 confirmados (classi_teste == 5) após 15 de fevereiro de 2020 (DT_SIN_PRI > "2020-02-15") com valor 0, e 1 para os outros casos
  mutate(obito_SRAG_TOTAL_P = ifelse(EVOLUCAO == 2, 1, 0)) %>% 
  mutate(evolucao_teste = ifelse(classi_nova == 5 & EVOLUCAO == 2 & DT_EVOLUCA < "2020-03-12", 0, 1)) %>%  #Cria uma nova variável 'evolucao_teste' que recebe valor 0 para óbitos por COVID-19 ocorridos antes de 12 de março de 2020 e 1 para os outros casos

  filter(evolucao_teste == 1) %>%   # Filtra os dados para incluir apenas os registros onde evolucao_teste é igual a 1, excluindo os óbitos por COVID-19 ocorridos antes de 12 de março de 2020
  replace_na(list(EVOLUCAO_teste = 0)) %>%  # Substitui valores NA na variável EVOLUCAO_teste por 0.
  mutate(indigena = ifelse(CS_RACA == 5, 1, 0), 
         tabagismo = ifelse(TABAG == 1, 1, 0))
         

</code></pre>
</div>
         
# Criar Faixas etárias (transformar formatos de datas)


<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">

SRAG_final <- SRAG_final %>%
  mutate(DT_NASC = parse_date_time(DT_NASC, orders = c("dmy", "ymd")),                 # Calcular a idade com base no valor de DT_NASC e DT_SIN_PRI   
         DT_SIN_PRI = parse_date_time(DT_SIN_PRI, orders = c("dmy", "ymd"))) %>%
 
  mutate(idade = as.numeric(difftime(DT_SIN_PRI, DT_NASC, units = "days")) / 365.25) %>%    
  mutate(categoria_dt_nasc = case_when(
    idade < 1 ~ "1. Menor que 1", 
    idade >= 1 & idade < 5 ~ "2. De 1 a 4 anos", 
    idade >= 5 & idade < 12 ~ "3. De 5 a 11 anos", 
    idade >= 12 & idade < 20 ~ "4. De 12 a 19 anos", 
    idade >= 20 & idade < 60 ~ "5. De 20 a 59 anos", 
    idade >= 60 & idade < 80 ~ "6. De 60 a 79 anos", 
    idade >= 80 ~ "7. De 80 para cima",
    TRUE ~ "Idade não especificada"  # Caso padrão para valores fora dos intervalos especificados
  ))

table(SRAG_final$categoria_dt_nasc)              # Verificar se a coluna foi criada corretamente

</code></pre>
</div>

# Padronização e criação de colunas 

<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">

SRAG_final <- SRAG_final %>% 
  
  mutate(caso_srag_por_covid = ifelse(classi_teste == 5 & caso_srag == 1, 1, 0)) %>%            # Identifica casos de SRAG causados por COVID-19

  mutate(variavel1 = ifelse(classi_teste == 5 & DT_SIN_PRI <= "2020-02-15", 0, 1)) %>%  
  
  filter(variavel1 == 1) %>%  
  
  mutate(obito_srag = ifelse(EVOLUCAO == 2, 1, 0)) %>%  
  
  mutate(EVOLUCAO_teste = ifelse(classi_teste == 5 & EVOLUCAO == 2 & DT_EVOLUCA < "2020-03-12", 0, 1)) %>%  
  
  filter(EVOLUCAO_teste == 1) %>%  
  
  mutate(obito_srag_por_covid = ifelse(classi_teste == 5 & EVOLUCAO == 2, 1, 0)) %>%   # mudando classe dos campos que compõe os fatores de risco/comorbidades 
  
  mutate(fator_risc = as.numeric(FATOR_RISC),            
         
         cardiopati = as.numeric(CARDIOPATI), 
         
         pneumopati = as.numeric(PNEUMOPATI), 
         
         diabetes = as.numeric(DIABETES), 
         
         obesidade = as.numeric(OBESIDADE), 
         
         neurologic = as.numeric(NEUROLOGIC), 
         
         renal = as.numeric(RENAL), 
         
         hepatica = as.numeric(HEPATICA), 
         
         sind_down = as.numeric(SIND_DOWN), 
         
         asma = as.numeric(ASMA), 
         
         imunodepre = as.numeric(IMUNODEPRE), 
         
         out_morbi = as.numeric(OUT_MORBI)) %>%  # Criando coluna fator_risc (Fatores de Risco)
  
  mutate(fator_risc = ifelse(fator_risc == 1, 1, 0), 
         
         cardiopati = ifelse(cardiopati == 1, 1, 0), 
         
         pneumopati = ifelse(pneumopati == 1, 1, 0), 
         
         diabetes = ifelse(diabetes == 1, 1, 0), 
         
         obesidade = ifelse(obesidade == 1, 1, 0), 
         
         neurologic = ifelse(neurologic == 1, 1, 0), 
         
         renal = ifelse(renal == 1, 1, 0), 
         
         hepatica = ifelse(hepatica == 1, 1, 0), 
         
         sind_down = ifelse(sind_down == 1, 1, 0), 
         
         asma = ifelse(asma == 1, 1, 0), 
         
         imunodepre = ifelse(imunodepre == 1, 1, 0), 
         
         out_morbi = ifelse(out_morbi == 1, 1, 0), 
         
         paxlovid = ifelse(TRAT_COV == 1 & TIPO_TRAT == 1, 1, 0)) %>%  
  
         mutate(CS_SEXO = case_when(CS_SEXO == "M" ~ "Masculino",  #   padronizando nomeclaturas 
                             
                             CS_SEXO == "F" ~ "Feminino", 
                             
                             CS_SEXO == "I" ~ "Sem Informação"), 
         
         CS_RACA = case_when(CS_RACA == 1 ~ "1. Branca", 
                             
                             CS_RACA == 2 ~ "2. Preta", 
                             
                             CS_RACA == 3 ~ "3. Amarela", 
                             
                             CS_RACA == 4 ~ "4. Parda", 
                             
                             CS_RACA == 5 ~ "5. Indígena", 
                             
                             CS_RACA == 9 ~ "6. Sem Informação")) %>%  
  
               mutate(REGIAO = case_when(SG_UF %in% c("DF", "MT", "MS", "GO") ~ "CO",         # criando coluna  para as regiões do Brasil 
                            
                            SG_UF %in% c("RS", "SC", "PR") ~ "S", 
                            
                            SG_UF %in% c("MG", "SP", "ES", "RJ") ~ "SE", 
                            
                            SG_UF %in% c("BA", "SE", "AL", "PE", "PB", "RN", "CE", "MA", "PI") ~ "NE", 
                            
                            SG_UF %in% c("TO", "RR", "RO", "PA", "AM", "AP", "AC") ~ "N")) %>%  
  
                mutate(tp_flu_pcr = as.numeric(TP_FLU_PCR),    # mudando a classe dos campos referentes aos testes 
         
         an_vsr = as.numeric(AN_VSR), 
         
         pcr_vsr = as.numeric(PCR_VSR), 
         
         an_para1 = as.numeric(AN_PARA1), 
         
         an_para2 = as.numeric(AN_PARA2), 
         
         an_para3 = as.numeric(AN_PARA3), 
         
         pcr_para1 = as.numeric(PCR_PARA1), 
         
         pcr_para2 = as.numeric(PCR_PARA2), 
         
         pcr_para3 = as.numeric(PCR_PARA3), 
         
         pcr_para4 = as.numeric(PCR_PARA4), 
         
         an_adeno = as.numeric(AN_ADENO), 
         
         pcr_adeno = as.numeric(PCR_ADENO), 
         
         an_outro = as.numeric(AN_OUTRO), 
         
         pcr_outro = as.numeric(PCR_OUTRO), 
         
         pcr_metap = as.numeric(PCR_METAP), 
         
         pcr_boca = as.numeric(PCR_BOCA), 
         
         pcr_rino = as.numeric(PCR_RINO), 
         
         tp_flu_an = as.numeric(TP_FLU_AN), 
         
         pcr_fluasu = as.numeric(PCR_FLUASU), 
         
         pcr_outro = as.numeric(PCR_OUTRO)) %>%  
  
        mutate(nova_flu = ifelse(tp_flu_an == 0 & tp_flu_pcr == 0 & classi_nova == 1, 1, 0)) %>%   # criando campo por meio da verificação dos resultados de cada teste, quando positivo > indica o vírus identificado  
  
      mutate(indic_vsr = ifelse(an_vsr == 1 | pcr_vsr == 1, 1, 0), 
         
         indic_para = ifelse(an_para1 == 1 | an_para2 == 1 | an_para3 == 1 | pcr_para1 == 1 |  
                               
                               pcr_para2 == 1 | pcr_para3 == 1 | pcr_para4 == 1, 1, 0), 
         
         indic_adeno = ifelse(an_adeno == 1 | pcr_adeno == 1, 1, 0),  
         
         indic_flub = ifelse(tp_flu_an == 2 | tp_flu_pcr == 2, 1, 0)) %>%  
  
          mutate(INFLUENZA_A_H1N1 = ifelse(pcr_fluasu == 1 & classi_teste != 5, 1, 0), 
         
         INFLUENZA_A_H3N2 = ifelse(pcr_fluasu == 2 & classi_teste != 5, 1, 0), 
         
         INFLUENZA_A_NAOSUB_I = ifelse(pcr_fluasu %in% c(3, 4, 5, 6) & classi_teste != 5, 1, 0), 
         
         INFLUENZA_SEM_TIPO = ifelse(is.na(tp_flu_an) & is.na(tp_flu_pcr) & classi_teste == 1, 1, 0), 
         
         INFLUENZA_SEM_TIPO_II = ifelse(classi_teste != 5 & nova_flu == 1, 1, 0), 
         
         INFLUENZA_A_NAOSUB_III = ifelse(tp_flu_an == 1 & classi_teste != 5, 1, 0), 
         
         INFLUENZA_B = ifelse(indic_flub == 1 & classi_teste != 5, 1, 0)) %>%  
  
          mutate(INFLUENZA_A_H1N1 = ifelse(is.na(INFLUENZA_A_H1N1), 0, INFLUENZA_A_H1N1), 
         
         INFLUENZA_A_H3N2 = ifelse(is.na(INFLUENZA_A_H3N2), 0, INFLUENZA_A_H3N2), 
         
         INFLUENZA_A_NAOSUB_I = ifelse(is.na(INFLUENZA_A_NAOSUB_I), 0, INFLUENZA_A_NAOSUB_I), 
         
         INFLUENZA_SEM_TIPO = ifelse(is.na(INFLUENZA_SEM_TIPO), 0, INFLUENZA_SEM_TIPO), 
         
         INFLUENZA_SEM_TIPO_II = ifelse(is.na(INFLUENZA_SEM_TIPO_II), 0, INFLUENZA_SEM_TIPO_II), 
         
         INFLUENZA_A_NAOSUB_III = ifelse(is.na(INFLUENZA_A_NAOSUB_III), 0, INFLUENZA_A_NAOSUB_III), 
         
         INFLUENZA_B = ifelse(is.na(INFLUENZA_B), 0, INFLUENZA_B)) %>%  
  
        mutate(INFLUENZA_A_NAOSUB = ifelse(INFLUENZA_A_NAOSUB_I == 1 | INFLUENZA_A_NAOSUB_III == 1 | INFLUENZA_SEM_TIPO == 1 | INFLUENZA_SEM_TIPO_II == 1, 1, 0)) %>%  
  
        mutate(SINCICIAL = ifelse(indic_vsr == 1 & classi_teste != 5 & INFLUENZA_A_H1N1 != 1 & INFLUENZA_A_H3N2 != 1 & INFLUENZA_A_NAOSUB != 1 & INFLUENZA_B != 1, 1, 0)) %>%  
  
        mutate(SINCICIAL = ifelse(is.na(SINCICIAL), 0, SINCICIAL)) %>%  
  
       mutate(ADENOVIRUS = ifelse(indic_adeno == 1 & classi_teste != 5 & INFLUENZA_A_H1N1 != 1 & INFLUENZA_A_H3N2 != 1 & INFLUENZA_A_NAOSUB != 1 & INFLUENZA_B != 1 & SINCICIAL != 1, 1, 0)) %>%  
  
        mutate(ADENOVIRUS = ifelse(is.na(ADENOVIRUS), 0, ADENOVIRUS)) %>%  
  
       mutate(RINOVIRUS = ifelse(pcr_rino == 1 & classi_teste != 5 & INFLUENZA_A_H1N1 != 1 & INFLUENZA_A_H3N2 != 1 & INFLUENZA_A_NAOSUB != 1 & INFLUENZA_B != 1 & SINCICIAL != 1 & ADENOVIRUS != 1, 1, 0)) %>%  
  
       mutate(RINOVIRUS = ifelse(is.na(RINOVIRUS), 0, RINOVIRUS)) %>%  
  
        mutate(PARAINFLUENZA = ifelse(indic_para == 1 & classi_teste != 5 & INFLUENZA_A_H1N1 != 1 & INFLUENZA_A_H3N2 != 1 & INFLUENZA_A_NAOSUB != 1 & INFLUENZA_B != 1 & SINCICIAL != 1 & ADENOVIRUS != 1 & RINOVIRUS != 1, 1, 0)) %>%  
  
       mutate(PARAINFLUENZA = ifelse(is.na(PARAINFLUENZA), 0, PARAINFLUENZA)) %>%  
  
       mutate(METAPNEUMO = ifelse(pcr_metap == 1 & classi_teste != 5 & INFLUENZA_A_H1N1 != 1 & INFLUENZA_A_H3N2 != 1 & INFLUENZA_A_NAOSUB != 1 & INFLUENZA_B != 1 & SINCICIAL != 1 & ADENOVIRUS != 1 & RINOVIRUS != 1 & PARAINFLUENZA != 1, 1, 0)) %>%  
  
      mutate(METAPNEUMO = ifelse(is.na(METAPNEUMO), 0, METAPNEUMO)) %>%  
  
      mutate(BOCAVIRUS = ifelse(pcr_boca == 1 & classi_teste != 5 & INFLUENZA_A_H1N1 != 1 & INFLUENZA_A_H3N2 != 1 & INFLUENZA_A_NAOSUB != 1 & INFLUENZA_B != 1 & SINCICIAL != 1 & ADENOVIRUS != 1 & RINOVIRUS != 1 & PARAINFLUENZA != 1 & METAPNEUMO != 1, 1, 0)) %>% 
  
      mutate(BOCAVIRUS = ifelse(is.na(BOCAVIRUS), 0, BOCAVIRUS)) %>%  
  
        mutate(antiviral = as.numeric(ANTIVIRAL), 
         
         mais_60 = ifelse(idade >= 60, 1, 0), 
         
         menos_6 = ifelse(idade <= 6, 1, 0)) %>%  
  
     mutate(POS_AN_FLU = ifelse(is.na(POS_AN_FLU), 0, POS_AN_FLU),    # substituir valores ausentes (NA) por zero em várias colunas do conjunto de dados 
         
         POS_PCRFLU = ifelse(is.na(POS_PCRFLU), 0, POS_PCRFLU), 
         
         an_para1 = ifelse(is.na(an_para1), 0, an_para1), 
         
         an_para2 = ifelse(is.na(an_para2), 0, an_para2), 
         
         an_para3 = ifelse(is.na(an_para3), 0, an_para3), 
         
         an_vsr = ifelse(is.na(an_vsr), 0, an_vsr), 
         
         an_adeno = ifelse(is.na(an_adeno), 0, an_adeno), 
         
         AN_SARS2 = ifelse(is.na(AN_SARS2), 0, AN_SARS2), 
         
         pcr_para1 = ifelse(is.na(pcr_para1), 0, pcr_para1), 
         
         pcr_para2 = ifelse(is.na(pcr_para2), 0, pcr_para2), 
         
         pcr_para3 = ifelse(is.na(pcr_para3), 0, pcr_para3), 
         
         pcr_para4 = ifelse(is.na(pcr_para4), 0, pcr_para4), 
         
         pcr_adeno = ifelse(is.na(pcr_adeno), 0, pcr_adeno), 
         
         pcr_metap = ifelse(is.na(pcr_metap), 0, pcr_metap), 
         
         pcr_boca = ifelse(is.na(pcr_boca), 0, pcr_boca), 
         
         PCR_SARS2 = ifelse(is.na(PCR_SARS2), 0, PCR_SARS2), 
         
         pcr_rino = ifelse(is.na(pcr_rino), 0, pcr_rino), 
         
         pcr_vsr = ifelse(is.na(pcr_vsr), 0, pcr_vsr), 
         
         pcr_outro = ifelse(is.na(pcr_outro), 0, pcr_outro)) %>%  
  
          mutate(N_ESPEC = ifelse(classi_teste == 4, 1, 0)) %>%  ## criando campos a partir da classificação do teste 
  
         mutate(EM_INVEST = ifelse(classi_teste == 0, 1, 0)) %>%  
  
        mutate(indic_pcr_outro = ifelse(pcr_outro == 1, 1, 0)) %>%  
  
        mutate(OUTROS_AG = ifelse(POS_AN_FLU != 1 & POS_PCRFLU != 1 & an_para1 != 1 & an_para2 != 1 & 
                              
                              an_para3 != 1 & an_vsr != 1 & an_adeno != 1 & AN_SARS2 != 1 & 
                              
                              pcr_para1 != 1 & pcr_para2 != 1 & pcr_para3 != 1 & pcr_para4 != 1 &      
                              
                              pcr_adeno != 1 & pcr_metap != 1 & pcr_boca != 1 & PCR_SARS2 != 1 & 
                              
                              pcr_rino != 1 & pcr_vsr != 1 & indic_pcr_outro != 1 & classi_teste == 3, 1, 0)) %>%  
  
             mutate(caso_srag_por_vsr = ifelse(caso_srag == 1 & SINCICIAL == 1, 1, 0), 
         
                                obito_srag_por_vsr = ifelse(caso_srag == 1 & SINCICIAL == 1 & EVOLUCAO == 2, 1, 0)) %>%   ## agregando todos os tipos de influenza em um campo só 
  
              mutate(INFLUENZA_TODAS = INFLUENZA_A_H1N1 + INFLUENZA_A_H3N2 + INFLUENZA_A_NAOSUB + INFLUENZA_B + INFLUENZA_A_NAOSUB, 
         
         OUTROS_VIRUS = PARAINFLUENZA + ADENOVIRUS + METAPNEUMO + BOCAVIRUS + RINOVIRUS + SINCICIAL) %>%  
  
         mutate(INFLUENZA_TODAS = ifelse(INFLUENZA_TODAS >= 1, 1, 0), 
         
         OUTROS_VIRUS = ifelse(OUTROS_VIRUS >= 1, 1, 0)) %>%  
  
            mutate(OUTROS_RESP = ifelse(POS_AN_FLU != 1 & POS_PCRFLU != 1 & an_para1 != 1 & an_para2 != 1 & 
                                
                                an_para3 != 1 & an_vsr != 1 & an_adeno != 1 & AN_SARS2 != 1 & 
                                
                                pcr_para1 != 1 & pcr_para2 != 1 & pcr_para3 != 1 & pcr_para4 != 1 &      
                                
                                pcr_adeno != 1 & pcr_metap != 1 & pcr_boca != 1 & PCR_SARS2 != 1 & 
                                
                                pcr_rino != 1 & pcr_vsr != 1 & indic_pcr_outro == 1 & classi_teste != 3, 1, 0)) %>%  
  
                  mutate(VIRUS_RESP = case_when(N_ESPEC == 1 ~ "NÃO ESPECIFICADA",   # atribuindo nome dos vírus/ diagnóstico
                                
                                EM_INVEST == 1 ~ "EM INVESTIGAÇÃO", 
                                
                                OUTROS_AG == 1 ~ "OUTROS AGENTES", 
                                
                                OUTROS_RESP == 1 ~ "OVR", 
                                
                                PARAINFLUENZA == 1 ~ "PARAINFLUENZA", 
                                
                                ADENOVIRUS == 1 ~ "ADENOVIRUS",  
                                
                                METAPNEUMO == 1 ~ "METAPNEUMO",  
                                
                                BOCAVIRUS == 1 ~ "BOCAVIRUS",  
                                
                                RINOVIRUS == 1 ~ "RINOVIRUS",  
                                
                                SINCICIAL == 1 ~ "SINCICIAL", 
                                
                                INFLUENZA_B == 1 ~ "INFLUENZA_B", 
                                
                                INFLUENZA_A_H1N1 == 1 ~ "INFLUENZA_A_H1N1",  
                                
                                INFLUENZA_A_H3N2 == 1 ~ "INFLUENZA_A_H3N2",  
                                
                                INFLUENZA_A_NAOSUB == 1 ~ "INFLUENZA_A_NAOSUB",  
                                
                                caso_srag_por_covid == 1 ~ "COVID-19")) %>%  
  
          mutate(VIRUS_RESP = ifelse(is.na(VIRUS_RESP) & classi_teste == 3, "OUTROS AGENTES", VIRUS_RESP)) %>%  # atribuindo valores a coluna vírus respiratórios  
  
        mutate(VIRUS_RESP = ifelse(is.na(VIRUS_RESP) & classi_teste == 2, "OVR", VIRUS_RESP)) %>%  
  
            mutate(classi_nova = case_when(VIRUS_RESP == "COVID-19" ~ "1. Covid-19", 
                                 
                                 VIRUS_RESP %in% c("INFLUENZA_A_H1N1", "INFLUENZA_A_H3N2", "INFLUENZA_A_NAOSUB", "INFLUENZA_B") ~ "2. Influenza", 
                                 
                                 VIRUS_RESP %in% c("PARAINFLUENZA", "ADENOVIRUS", "METAPNEUMO", "BOCAVIRUS", "RINOVIRUS", "SINCICIAL", "OVR") ~ "3. Outros Vírus Respiratórios", 
                                 
                                 VIRUS_RESP == "OUTROS AGENTES" ~ "4. Outros Agentes Etiológicos", 
                                 
                                 VIRUS_RESP == "NÃO ESPECIFICADA" ~ "5. Não Especificada", 
                                 
                                 VIRUS_RESP == "EM INVESTIGAÇÃO" ~ "6. Em Investigação")) %>%  
  
              mutate(INFLUENZA_A_H1N1_caso = ifelse(VIRUS_RESP == "INFLUENZA_A_H1N1" & caso_srag == 1, 1, 0), 
         
         INFLUENZA_A_H3N2_caso = ifelse(VIRUS_RESP == "INFLUENZA_A_H3N2" & caso_srag == 1, 1, 0), 
         
         INFLUENZA_A_NAOSUB_caso = ifelse(VIRUS_RESP == "INFLUENZA_A_NAOSUB" & caso_srag == 1, 1, 0), 
         
         INFLUENZA_B_caso = ifelse(VIRUS_RESP == "INFLUENZA_B" & caso_srag == 1, 1, 0), 
         
         SINCICIAL_caso = ifelse(VIRUS_RESP == "SINCICIAL" & caso_srag == 1, 1, 0), 
         
         PARAINFLUENZA_caso = ifelse(VIRUS_RESP == "PARAINFLUENZA" & caso_srag == 1, 1, 0), 
         
         ADENOVIRUS_caso = ifelse(VIRUS_RESP == "ADENOVIRUS" & caso_srag == 1, 1, 0), 
         
         METAPNEUMO_caso = ifelse(VIRUS_RESP == "METAPNEUMO" & caso_srag == 1, 1, 0), 
         
         BOCAVIRUS_caso = ifelse(VIRUS_RESP == "BOCAVIRUS" & caso_srag == 1, 1, 0), 
         
         RINOVIRUS_caso = ifelse(VIRUS_RESP == "RINOVIRUS" & caso_srag == 1, 1, 0), 
         
         COVID_caso = ifelse(VIRUS_RESP == "COVID-19" & caso_srag == 1, 1, 0), 
         
         N_ESPEC_caso = ifelse(VIRUS_RESP == "NÃO ESPECIFICADA" & caso_srag == 1, 1, 0), 
         
         EM_INVEST_caso = ifelse(VIRUS_RESP == "EM INVESTIGAÇÃO" & caso_srag == 1, 1, 0), 
         
         OUTROS_AG_caso = ifelse(VIRUS_RESP == "OUTROS AGENTES" & caso_srag == 1, 1, 0), 
         
         OVR_caso = ifelse(VIRUS_RESP == "OVR" & caso_srag == 1, 1, 0)) %>%  
  
            mutate(INFLUENZA_A_H1N1_obito = ifelse(VIRUS_RESP == "INFLUENZA_A_H1N1" & obito_srag == 1, 1, 0), 
         
         INFLUENZA_A_H3N2_obito = ifelse(VIRUS_RESP == "INFLUENZA_A_H3N2" & obito_srag == 1, 1, 0), 
         
         INFLUENZA_A_NAOSUB_obito = ifelse(VIRUS_RESP == "INFLUENZA_A_NAOSUB" & obito_srag == 1, 1, 0), 
         
         INFLUENZA_B_obito = ifelse(VIRUS_RESP == "INFLUENZA_B" & obito_srag == 1, 1, 0), 
         
         SINCICIAL_obito = ifelse(VIRUS_RESP == "SINCICIAL" & obito_srag == 1, 1, 0), 
         
         PARAINFLUENZA_obito = ifelse(VIRUS_RESP == "PARAINFLUENZA" & obito_srag == 1, 1, 0), 
         
         ADENOVIRUS_obito = ifelse(VIRUS_RESP == "ADENOVIRUS" & obito_srag == 1, 1, 0), 
         
         METAPNEUMO_obito = ifelse(VIRUS_RESP == "METAPNEUMO" & obito_srag == 1, 1, 0), 
         
         BOCAVIRUS_obito = ifelse(VIRUS_RESP == "BOCAVIRUS" & obito_srag == 1, 1, 0), 
         
         RINOVIRUS_obito = ifelse(VIRUS_RESP == "RINOVIRUS" & obito_srag == 1, 1, 0), 
         
         COVID_obito = ifelse(VIRUS_RESP == "COVID-19" & obito_srag == 1, 1, 0), 
         
         N_ESPEC_obito = ifelse(VIRUS_RESP == "NÃO ESPECIFICADA" & obito_srag == 1, 1, 0), 
         
         EM_INVEST_obito = ifelse(VIRUS_RESP == "EM INVESTIGAÇÃO" & obito_srag == 1, 1, 0), 
         
         OUTROS_AG_obito = ifelse(VIRUS_RESP == "OUTROS AGENTES" & obito_srag == 1, 1, 0), 
         
         OVR_obito = ifelse(VIRUS_RESP == "OVR" & obito_srag == 1, 1, 0)) %>%  
  
              mutate(INFLUENZA_caso = ifelse(classi_nova == "2. Influenza", 1, 0), 
         
         INFLUENZA_obito = ifelse(classi_nova == "2. Influenza" & EVOLUCAO == 2, 1, 0))   

</code></pre>
</div>


# Filtrar apenas quem atende a definição de caso

<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">


SRAG_filtrado2 <- SRAG_final %>% 
  filter(caso_srag == "1")
  
  </code></pre>
</div>

# Criar as tabelas para casos com caracteristicas de pessoas

<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">

TABELA1_SRAG_CLASSIFICACAO_CASOS <- SRAG_filtrado2 %>% 
  dcast(caso_srag + ANO ~ classi_nova, value.var = "caso_srag")

TABELA2_SRAG_FX_ET_CASOS <- SRAG_filtrado2 %>% 
  filter(ANO == "2024") %>% 
  dcast(categoria_dt_nasc ~ classi_nova, value.var = "caso_srag") %>%
  mutate(varivel = categoria_dt_nasc) %>% 
  select(-c(categoria_dt_nasc))

TABELA2_SRAG_SEXO_CASOS <- SRAG_filtrado2 %>% 
  filter(ANO == "2024") %>% 
  dcast(CS_SEXO ~ classi_nova, value.var = "caso_srag") %>% 
  mutate(varivel = CS_SEXO) %>% 
  select(-c(CS_SEXO))

TABELA2_SRAG_RACA_CASOS <- SRAG_filtrado2 %>% 
  filter(ANO == "2024") %>% 
  dcast(CS_RACA ~ classi_nova, value.var = "caso_srag") %>% 
  mutate(varivel = CS_RACA) %>% 
  select(-c(CS_RACA))

# Unir as tabelas de casos
TABELA_UNIDA_CASOS <- bind_rows(
  TABELA1_SRAG_CLASSIFICACAO_CASOS,
  TABELA2_SRAG_FX_ET_CASOS,
  TABELA2_SRAG_SEXO_CASOS,
  TABELA2_SRAG_RACA_CASOS
) %>% relocate(varivel, .before = 1) # Colocar a coluna varivel em primeiro 

</code></pre>
</div>

# Criar as tabelas de características de pessoas para os óbitos

<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">

TABELA1_SRAG_CLASSIFICACAO_OBITOS <- SRAG_filtrado2 %>% 
  dcast(obito_srag + ANO ~ classi_nova, value.var = "obito_srag")

TABELA2_SRAG_FX_ET_OBITOS <- SRAG_filtrado2 %>% 
  filter(ANO == "2024") %>% 
  dcast(categoria_dt_nasc ~ classi_nova, value.var = "obito_srag") %>%
  mutate(varivel = categoria_dt_nasc) %>% 
  select(-c(categoria_dt_nasc))

TABELA2_SRAG_SEXO_OBITOS <- SRAG_filtrado2 %>% 
  filter(ANO == "2024") %>% 
  dcast(CS_SEXO ~ classi_nova, value.var = "obito_srag") %>% 
  mutate(varivel = CS_SEXO) %>% 
  select(-c(CS_SEXO))

TABELA2_SRAG_RACA_OBITOS <- SRAG_filtrado2 %>% 
  filter(ANO == "2024") %>% 
  dcast(CS_RACA ~ classi_nova, value.var = "obito_srag") %>% 
  mutate(varivel = CS_RACA) %>% 
  select(-c(CS_RACA))

# Unir as tabelas de óbitos
TABELA_UNIDA_OBITOS <- bind_rows(
  TABELA1_SRAG_CLASSIFICACAO_OBITOS,
  TABELA2_SRAG_FX_ET_OBITOS,
  TABELA2_SRAG_SEXO_OBITOS,
  TABELA2_SRAG_RACA_OBITOS
) %>% relocate(varivel, .before = 1) # Colocar a coluna varivel em primeiro


</code></pre>
</div>

<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">

# Criar o workbook e adicionar as tabelas em abas separadas
wb <- createWorkbook()
addWorksheet(wb, "Casos")
addWorksheet(wb, "Óbitos")

writeData(wb, sheet = "Casos", TABELA_UNIDA_CASOS)
writeData(wb, sheet = "Óbitos", TABELA_UNIDA_OBITOS)


saveWorkbook(wb, includeHTML("Caderno_de_Analise_SRAG_SIVEP.html"))  # Salvar o arquivo Excel

</code></pre>
</div>

# Criar pirâmide de gênero e faixa etária dos casos de SRAG

<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">

dados_piramide <- SRAG_filtrado2 %>%                # Agrupar os dados por faixa etária e sexo e contar os casos
  filter(!is.na(categoria_dt_nasc) & !is.na(CS_SEXO)) %>%
  filter(categoria_dt_nasc != "Idade não especificada") %>%
  group_by(categoria_dt_nasc, CS_SEXO) %>%
  summarise(casos = sum(caso_srag, na.rm = TRUE)) %>%
  ungroup()


dados_piramide <- dados_piramide %>% # Ajustar os valores para negativo para o sexo feminino para a pirâmide etária
  mutate(casos = ifelse(CS_SEXO == "Feminino", -casos, casos))


ordenar_faixas <- c("1. Menor que 1", "2. De 1 a 4 anos", "3. De 5 a 11 anos",            # Definir a ordem das faixas etárias
                    "4. De 12 a 19 anos", "5. De 20 a 59 anos", "6. De 60 a 79 anos", 
                    "7. 80 para cima")
dados_piramide$categoria_dt_nasc <- factor(dados_piramide$categoria_dt_nasc, levels = ordenar_faixas)


piramide_srag <- ggplot(dados_piramide, aes(x = categoria_dt_nasc, y = casos, fill = CS_SEXO)) +              # Criar o gráfico de pirâmide etária
  geom_bar(stat = "identity", position = "stack") +
  coord_flip() +
  scale_fill_manual(values = c("Feminino" = "#F4A460", "Masculino" = "#F5DEB3")) +
  labs(title = "Pirâmide Etária dos Casos de SRAG",
       x = "Faixa Etária",
       y = "Número de Casos",
       fill = "Gênero") +
  theme_minimal() +
  scale_y_continuous(labels = abs)


print(piramide_srag)  # Exibir o gráfico


ggsave(filename = includeHTML("Caderno_de_Analise_SRAG_SIVEP.html")
, plot = piramide_srag, width = 10, height = 6, units = "in", dpi = 300)           # Salvar o gráfico em um arquivo


</code></pre>
</div>

#GRAFICO CASOS DE SRAg por COVID POR SEMANA com média móvel

<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">

GRAFICO_CASOS_COVID_SE <- SRAG_filtrado2 %>% 
  filter(SEM_PRI != "2019_50") %>%              ####   ,SG_UF == "SP"   inserir filtro de UF
  mutate(uti_covid = ifelse(UTI == 1 & caso_srag_por_covid == 1, 1, 0)) %>% 
  group_by(SEM_PRI) %>% 
  summarise(`Casos Covid-19 Total`  = sum(COVID_caso, na.rm = T),
            `Óbitos SRAG por Covid-19` = sum(COVID_obito, na.rm = T)) %>% 
  mutate(`Casos SRAG por Covid-19` = `Casos Covid-19 Total` - `Óbitos SRAG por Covid-19`) %>% 
  mutate(`Letalidade de SRAG por Covid-19` = `Óbitos SRAG por Covid-19`/`Casos SRAG por Covid-19`) %>% 
  select(SEM_PRI, `Casos Covid-19 Total`, `Óbitos SRAG por Covid-19`, `Casos SRAG por Covid-19`,
         `Letalidade de SRAG por Covid-19`)

write.csv2 (GRAFICO_CASOS_COVID_SE,includeHTML("Caderno_de_Analise_SRAG_SIVEP.html")")

# Calcular a média móvel de 4 semanas (28 dias)
GRAFICO_CASOS_COVID_SE <- GRAFICO_CASOS_COVID_SE %>%
  arrange(SEM_PRI) %>%
  mutate(`Média Móvel 4 Semanas` = rollmean(`Casos Covid-19 Total`, k = 4, fill = NA, align = "right"))


# Criar o gráfico de barras com a média móvel
GRAFICO_CASOS_COVID_SE <- ggplot(GRAFICO_CASOS_COVID_SE, aes(x = as.factor(SEM_PRI), y = `Casos Covid-19 Total`)) +
  geom_bar(stat = "identity", fill = "steelblue", alpha = 0.7) +
  geom_line(aes(y = `Média Móvel 4 Semanas`, group = 1), color = "red", size = 1) +
  geom_point(aes(y = `Média Móvel 4 Semanas`), color = "red", size = 2) +
  geom_text(aes(y = `Média Móvel 4 Semanas`, label = round(`Média Móvel 4 Semanas`, 1)), 
            vjust = -0.5, color = "red", size = 3) +
  labs(title = "Casos de SRAG por Covid-19 por Semana Epidemiológica",
       subtitle = "Com Média Móvel de 4 Semanas",
       x = "Semana Epidemiológica",
       y = "Número de Casos",
       caption = "Fonte: SRAG_filtrado2") +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 90, hjust = 1))

print(GRAFICO_CASOS_COVID_SE)  ## mostrar o grafico

# Salvar o gráfico em um arquivo
ggsave(filename = includeHTML("Caderno_de_Analise_SRAG_SIVEP.html")
, plot = GRAFICO_CASOS_COVID_SE, width = 10, height = 6, units = "in", dpi = 300)

</code></pre>
</div>

# Gráfico óbitos de SRAG por covid-19 COM MÉDIA MÒVEL

<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">

# Filtrar os dados para óbitos e calcular a média móvel
GRAFICO_OBITOS_COVID_SE <- SRAG_filtrado2 %>%
  filter(SEM_PRI != "2019_50" & EVOLUCAO == "2") %>% # Filtrar apenas os óbitos e excluir semana específica
  mutate(uti_covid = ifelse(UTI == 1 & caso_srag_por_covid == 1, 1, 0)) %>%
  group_by(SEM_PRI) %>%
  summarise(`Óbitos SRAG por Covid-19` = sum(COVID_obito, na.rm = TRUE)) %>%
  arrange(SEM_PRI) %>%
  mutate(`Média Móvel 4 Semanas` = rollmean(`Óbitos SRAG por Covid-19`, k = 4, fill = NA, align = "right"))

# Criar o gráfico de barras com a média móvel
grafico_obitos_covid_SE <- ggplot(GRAFICO_OBITOS_COVID_SE, aes(x = as.factor(SEM_PRI), y = `Óbitos SRAG por Covid-19`)) +
  geom_bar(stat = "identity", fill = "#FA8072", color = "red", alpha = 0.7) +
  geom_line(aes(y = `Média Móvel 4 Semanas`, group = 1), color = "red", size = 1) +
  geom_point(aes(y = `Média Móvel 4 Semanas`), color = "red", size = 2) +
  geom_text(aes(y = `Média Móvel 4 Semanas`, label = round(`Média Móvel 4 Semanas`, 1)), 
            vjust = -0.5, color = "red", size = 3) +
  labs(title = "Óbitos por SRAG por Covid-19 por Semana Epidemiológica",
       subtitle = "Com Média Móvel de 4 Semanas",
       x = "Semana Epidemiológica",
       y = "Número de Óbitos",
       caption = "Fonte: SRAG_filtrado2") +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 90, hjust = 1))

# Exibir o gráfico
print(grafico_obitos_covid_SE)

# Salvar o gráfico em um arquivo
ggsave(filename = includeHTML("Caderno_de_Analise_SRAG_SIVEP.html")
, plot = grafico_obitos_covid_SE, width = 10, height = 6, units = "in", dpi = 300)

</code></pre>
</div>

# GRAFICO TENDENCIA TODOS OS VIRUS - Casos 

<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">

total_srag_semana <- SRAG_filtrado2 %>%
  group_by(SEM_PRI) %>%
  summarize(Total_SRAG = n())

# Calcular a contagem de casos para cada vírus por semana epidemiológica
contagem_virus_semana <- SRAG_filtrado2 %>%
  mutate(SEM_PRI = factor(SEM_PRI, levels = unique(SEM_PRI), ordered = TRUE)) %>%
  group_by(SEM_PRI) %>%
  summarize(
    SINCICIAL_caso = sum(SINCICIAL_caso, na.rm = TRUE),
    INFLUENZA_caso = sum(INFLUENZA_caso, na.rm = TRUE),
    COVID_caso = sum(COVID_caso, na.rm = TRUE),
    RINOVIRUS_caso = sum(RINOVIRUS_caso, na.rm = TRUE),
    OVR_caso = sum(PARAINFLUENZA_caso + ADENOVIRUS_caso + BOCAVIRUS_caso + METAPNEUMO_caso + OVR_caso, na.rm = TRUE)
  )

# Converter SEM_PRI para o mesmo tipo em ambas as tabelas
total_srag_semana$SEM_PRI <- as.character(total_srag_semana$SEM_PRI)
contagem_virus_semana$SEM_PRI <- as.character(contagem_virus_semana$SEM_PRI)

# Renomear colunas para a legenda
colnames(contagem_virus_semana) <- c("SEM_PRI", "VSR", "Influenza geral", "Covid-19", "Rinovírus", "OVR")

# Combinar os dados
dados_completos <- total_srag_semana %>%
  left_join(contagem_virus_semana, by = "SEM_PRI") %>%
  pivot_longer(cols = c("VSR", "Influenza geral", "Covid-19", "Rinovírus", "OVR"), 
               names_to = "Virus", values_to = "Contagem") %>%
  mutate(Proporcao = Contagem / Total_SRAG * 100)

# Ordenar SEM_PRI como numérico para garantir que a última semana seja selecionada corretamente
dados_completos$SEM_PRI <- as.numeric(as.character(dados_completos$SEM_PRI))

# Verificar a última semana para garantir que a proporção está correta
dados_ultima_semana <- dados_completos %>%
  filter(SEM_PRI == max(SEM_PRI))

# Ajuste para melhorar a posição dos rótulos de proporção
GRAFICO_TEND_CASOS <- ggplot() +
  geom_bar(data = total_srag_semana, aes(x = as.numeric(SEM_PRI), y = Total_SRAG, fill = "Total de Casos de SRAG"), stat = "identity", alpha = 0.5, width = 1, color = "blue") +
  geom_text(data = total_srag_semana, aes(x = as.numeric(SEM_PRI), y = Total_SRAG, label = Total_SRAG), vjust = -0.5, size = 3, show.legend = FALSE) +
  geom_line(data = dados_completos, aes(x = as.numeric(SEM_PRI), y = Proporcao * max(total_srag_semana$Total_SRAG) / 50, color = Virus), size = 1) +
  geom_point(data = dados_completos, aes(x = as.numeric(SEM_PRI), y = Proporcao * max(total_srag_semana$Total_SRAG) / 50, color = Virus), size = 2) +
  geom_text(data = dados_ultima_semana, aes(x = as.numeric(SEM_PRI), y = Proporcao * max(total_srag_semana$Total_SRAG) / 50, label = percent(Proporcao / 100, accuracy = 0.1), color = Virus), 
            size = 3, vjust = -0.5, hjust = -0.3, show.legend = FALSE) +
  scale_y_continuous(
    name = "Número de Casos de SRAG",
    limits = c(0, max(total_srag_semana$Total_SRAG) * 1.1),  # Ajustar conforme necessário para acomodar todos os dados
    sec.axis = sec_axis(~./max(total_srag_semana$Total_SRAG) * 50, name = "Proporção de Casos (%)", breaks = seq(0, 50, by = 10), labels = function(b) paste0(b, "%"))
  ) +
  scale_x_continuous(breaks = unique(as.numeric(dados_completos$SEM_PRI))) +
  scale_fill_manual(values = "#87CEFA", labels = "Total de Casos de SRAG") +
  labs(
    title = "Casos de SRAG e Proporção de Agentes por Semana Epidemiológica",
    x = "Semana Epidemiológica",
    color = "",
    fill = ""
  ) +
  theme_economist() +
  theme(
    panel.background = element_rect(fill = "white", color = NA),
    plot.background = element_rect(fill = "white", color = NA),
    axis.line = element_line(color = "black", size = 1),
    panel.grid.major = element_line(color = "grey80"),
    panel.grid.minor = element_line(color = "grey90"),
    axis.ticks = element_line(color = "black")
  )

print(GRAFICO_TEND_CASOS )

# Salvar o gráfico em um arquivo
ggsave(filename = includeHTML("Caderno_de_Analise_SRAG_SIVEP.html")
, plot = GRAFICO_TEND_CASOS, width = 10, height = 6, units = "in", dpi = 300)

</code></pre>
</div>

# GRAFICO TENDENCIA TODOS OS VIRUS - Óbitos

<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">

# Filtrar os dados para óbitos (evolucao == 2)
SRAG_filtrado_obitos <- SRAG_filtrado2 %>%
  filter(EVOLUCAO == 2)

# Agrupar dados de óbitos por semana epidemiológica
total_obitos_semana <- SRAG_filtrado_obitos %>%
  group_by(SEM_PRI) %>%
  summarize(Total_Obitos = n())

# Calcular a contagem de casos para cada vírus por semana epidemiológica
contagem_virus_semana_obitos <- SRAG_filtrado_obitos %>%
  mutate(SEM_PRI = factor(SEM_PRI, levels = unique(SEM_PRI), ordered = TRUE)) %>%
  group_by(SEM_PRI) %>%
  summarize(
    SINCICIAL_caso = sum(SINCICIAL_caso, na.rm = TRUE),
    INFLUENZA_caso = sum(INFLUENZA_caso, na.rm = TRUE),
    COVID_caso = sum(COVID_caso, na.rm = TRUE),
    RINOVIRUS_caso = sum(RINOVIRUS_caso, na.rm = TRUE),
    OVR_caso = sum(PARAINFLUENZA_caso + ADENOVIRUS_caso + BOCAVIRUS_caso + METAPNEUMO_caso + OVR_caso, na.rm = TRUE)
  )

# Converter SEM_PRI para o mesmo tipo em ambas as tabelas
total_obitos_semana$SEM_PRI <- as.character(total_obitos_semana$SEM_PRI)
contagem_virus_semana_obitos$SEM_PRI <- as.character(contagem_virus_semana_obitos$SEM_PRI)

# Renomear colunas para a legenda
colnames(contagem_virus_semana_obitos) <- c("SEM_PRI", "VSR", "Influenza geral", "Covid-19", "Rinovírus", "OVR")

# Combinar os dados
dados_completos_obitos <- total_obitos_semana %>%
  left_join(contagem_virus_semana_obitos, by = "SEM_PRI") %>%
  pivot_longer(cols = c("VSR", "Influenza geral", "Covid-19", "Rinovírus", "OVR"), 
               names_to = "Virus", values_to = "Contagem") %>%
  mutate(Proporcao = ifelse(Total_Obitos == 0, NA, Contagem / Total_Obitos * 100))

# Ordenar SEM_PRI como numérico para garantir que a última semana seja selecionada corretamente
dados_completos_obitos$SEM_PRI <- as.numeric(as.character(dados_completos_obitos$SEM_PRI))

# Verificar a última semana para garantir que a proporção está correta
dados_ultima_semana_obitos <- dados_completos_obitos %>%
  filter(SEM_PRI == max(SEM_PRI))

# Ajuste para melhorar a posição dos rótulos de proporção
# Ajuste para melhorar a posição dos rótulos de proporção
GRAFICO_TEND_OBITOS <- ggplot() +
  geom_bar(data = total_obitos_semana, aes(x = as.numeric(SEM_PRI), y = Total_Obitos, fill = "Total de Óbitos de SRAG"), stat = "identity", alpha = 0.5, width = 1, color = "#CD5C5C") +
  geom_text(data = total_obitos_semana, aes(x = as.numeric(SEM_PRI), y = Total_Obitos, label = Total_Obitos), vjust = -0.5, size = 3, show.legend = FALSE) +
  geom_line(data = dados_completos_obitos, aes(x = as.numeric(SEM_PRI), y = Proporcao * max(total_obitos_semana$Total_Obitos, na.rm = TRUE) / 70, color = Virus), size = 1) +
  geom_point(data = dados_completos_obitos, aes(x = as.numeric(SEM_PRI), y = Proporcao * max(total_obitos_semana$Total_Obitos, na.rm = TRUE) / 70, color = Virus), size = 2) +
  geom_text(data = dados_ultima_semana_obitos, aes(x = as.numeric(SEM_PRI), y = Proporcao * max(total_obitos_semana$Total_Obitos, na.rm = TRUE) / 70, label = percent(Proporcao / 100, accuracy = 0.1), color = Virus), 
            size = 3, vjust = -0.5, hjust = -0.3, show.legend = FALSE) +
  scale_y_continuous(
    name = "Número de Óbitos de SRAG",
    limits = c(0, max(total_obitos_semana$Total_Obitos, na.rm = TRUE) * 1.1),  # Ajustar conforme necessário para acomodar todos os dados
    sec.axis = sec_axis(~./max(total_obitos_semana$Total_Obitos, na.rm = TRUE) * 70, name = "Proporção de Óbitos (%)", breaks = seq(0, 70, by = 10), labels = function(b) paste0(b, "%"))
  ) +
  scale_x_continuous(breaks = unique(as.numeric(dados_completos_obitos$SEM_PRI))) +
  scale_fill_manual(values = "#F08080", labels = "Total de Óbitos de SRAG") +
  labs(
    title = "Óbitos de SRAG e Proporção de Agentes por Semana Epidemiológica",
    x = "Semana Epidemiológica",
    color = "",
    fill = ""
  ) +
  theme_economist() +
  theme(
    panel.background = element_rect(fill = "white", color = NA),
    plot.background = element_rect(fill = "white", color = NA),
    axis.line = element_line(color = "black", size = 1),
    panel.grid.major = element_line(color = "grey80"),
    panel.grid.minor = element_line(color = "grey90"),
    axis.ticks = element_line(color = "black")
  )


print(GRAFICO_TEND_OBITOS)

# Salvar o gráfico em um arquivo
ggsave(filename =includeHTML("Caderno_de_Analise_SRAG_SIVEP.html")
, plot = GRAFICO_TEND_OBITOS, width = 10, height = 6, units = "in", dpi = 300)

</code></pre>
</div>

#  GRAFICO DUNET AMOSTRAS

<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">

# Preparar os dados
dados_amostra <- SRAG_filtrado2 %>%
  filter(AMOSTRA %in% c("1", "2", "9")) %>%
  mutate(AMOSTRA = case_when(
    AMOSTRA == "1" ~ "Coletada",
    AMOSTRA == "2" ~ "Não Coletada",
    AMOSTRA == "9" ~ "Ignorado"
  )) %>%
  count(AMOSTRA)

# Calcular a posição dos rótulos para evitar sobreposição
dados_amostra <- dados_amostra %>%
  arrange(desc(AMOSTRA)) %>%
  mutate(pos = cumsum(n) - n / 2)

# Criar o gráfico do tipo donut (rosca)
grafico_donut <- ggplot(dados_amostra, aes(x = 2, y = n, fill = AMOSTRA)) +
  geom_bar(stat = "identity", width = 1) +
  coord_polar(theta = "y") +
  geom_label_repel(aes(label = scales::percent(n / sum(n), accuracy = 0.1), y = pos), 
                   color = "black", size = 5, box.padding = 0.3, nudge_x = 0.5, show.legend = FALSE) +
  geom_segment(aes(y = pos, yend = pos, x = 2, xend = 2.4), color = "black") +
  scale_fill_manual(values = c("Coletada" = "#4CAF50", "Não Coletada" = "#FF5722", "Ignorado" = "#FFC107")) +
  labs(
    title = "Distribuição de Amostras Coletadas, Não Coletadas e Ignoradas",
    fill = "Status da Amostra"
  ) +
  theme_void() +
  theme(
    plot.title = element_text(hjust = 0.5, size = 16, face = "bold"),
    legend.title = element_text(size = 12),
    legend.text = element_text(size = 10)
  ) +
  xlim(0.5, 4)

# Exibir o gráfico
print(grafico_donut)

# Salvar o gráfico em um arquivo
ggsave(filename = print(GRAFICO_TEND_OBITOS)

# Salvar o gráfico em um arquivo
ggsave(filename =includeHTML("Caderno_de_Analise_SRAG_SIVEP.html")
, plot = GRAFICO_TEND_OBITOS, width = 10, height = 6, units = "in", dpi = 300),
       plot = grafico_donut, width = 10, height = 6, units = "in", dpi = 300)
       

</code></pre>
</div>

# Gráfico Tipo de Testes 
<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">

# Preparar os dados considerando os três tipos de testes
dados_testes <- SRAG_filtrado2 %>%
  mutate(
    Teste = case_when(
      TP_TES_AN == 1 ~ "Imunofluorescência (IF)",
      TP_TES_AN == 2 ~ "Teste rápido antigênico",
      PCR_RESUL %in% c(1, 2, 3, 5) ~ "PCR",
      TRUE ~ NA_character_
    )
  ) %>%
  filter(!is.na(Teste)) %>%
  count(Teste)

# Calcular a posição dos rótulos para evitar sobreposição
dados_testes <- dados_testes %>%
  arrange(desc(Teste)) %>%
  mutate(pos = cumsum(n) - n / 2)

# Calcular total de amostras testadas
total_amostras <- sum(dados_testes$n)

# Criar rótulos da legenda com total de amostras para cada teste
dados_testes <- dados_testes %>%
  mutate(Teste_label = paste0(Teste, " (n=", n, ")"))

# Criar gráfico donut com as proporções de amostras testadas com cada tipo de teste
grafico_donut_testes <- ggplot(dados_testes, aes(x = 2, y = n, fill = Teste_label)) +
  geom_bar(stat = "identity", width = 1) +
  coord_polar(theta = "y") +
  geom_label_repel(aes(label = scales::percent(n / sum(n), accuracy = 0.1), y = pos, x = 2.5), 
                   color = "black", size = 5, box.padding = 0.3, nudge_x = 0.5, show.legend = FALSE) +
  geom_segment(aes(y = pos, yend = pos, x = 2, xend = 2.4), color = "black") +
  scale_fill_manual(values = c("#4CAF50", "#FF5722", "#03A9F4")) +
  labs(
    title = paste("Proporções de Amostras Testadas com Cada Tipo de Teste (Total: n=", total_amostras, ")", sep=""),
    fill = "Tipo de Teste"
  ) +
  theme_void() +
  theme(
    plot.title = element_text(hjust = 0.5, size = 16, face = "bold"),
    legend.title = element_text(size = 12),
    legend.text = element_text(size = 10)
  ) +
  xlim(0.5, 4)

# Exibir o gráfico
print(grafico_donut_testes)

# Salvar o gráfico
ggsave(filename = print(GRAFICO_TEND_OBITOS)

# Salvar o gráfico em um arquivo
ggsave(filename =includeHTML("Caderno_de_Analise_SRAG_SIVEP.html")
, plot = GRAFICO_TEND_OBITOS, width = 10, height = 6, units = "in", dpi = 300), plot = grafico_donut_testes, width = 10, height = 6, units = "in", dpi = 300)


</code></pre>
</div>

# MAPAS     

<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">
# Contar os casos de SRAG por município no estado de São Paulo
casos_por_municipio <- SRAG_filtrado2 %>%
  filter(SG_UF_NOT == "SP") %>%
  group_by(CO_MUN_NOT) %>%
  summarise(casos_srag = n()) %>%
  ungroup()

# Converter COD_MUN_NOT para numérico
casos_por_municipio <- casos_por_municipio %>%
  mutate(CO_MUN_NOT = as.numeric(as.character(CO_MUN_NOT)))

# Carregar os dados geográficos dos municípios de São Paulo
municipios_sp <- read_municipality(code_muni = "SP", year = 2020)

# Remover o último dígito de code_muni
municipios_sp <- municipios_sp %>%
  mutate(code_muni_short = as.numeric(substr(as.character(code_muni), 1, nchar(as.character(code_muni)) - 1)))

# Adicionar dados de casos ao shapefile
municipios_sp <- municipios_sp %>%
  left_join(casos_por_municipio, by = c("code_muni_short" = "CO_MUN_NOT"))

# Definir coordenadas centrais para as bolhas
municipios_sp_centroides <- municipios_sp %>%
  st_centroid() %>%
  st_coordinates() %>%
  as.data.frame() %>%
  rename(lon = X, lat = Y)

municipios_sp <- cbind(municipios_sp, municipios_sp_centroides)

# Mapa de bolhas para os municípios de São Paulo
mapa_bolhas_sp <- ggplot(data = municipios_sp) +
  geom_sf(fill = "white", color = "black") +
  geom_point(aes(x = lon, y = lat, size = casos_srag, color = casos_srag), alpha = 0.6) +
  scale_size_continuous(range = c(3, 20), guide = 'none') + # Remover a legenda de tamanhos
  scale_color_viridis_c(option = "plasma", direction = -1) +
  theme_void() +
  labs(title = "Casos de SRAG por Município em São Paulo", color = "Casos de SRAG")

print(mapa_bolhas_sp)

# Salvar o gráfico
ggsave("mapa_bolhas_sp.png", mapa_bolhas_sp, width = 10, height = 8)


</code></pre>
</div>


# CASOS COM IDENTIFICAÇÃO DE VIRUS RESPIRATORIOS POREM SEM CLASSIFICAÇÃO DE SRAG 

<div class="code-box">
<button class="btn btn-primary" onclick="copyToClipboard('#diretorio')">Copiar Código</button>
<pre id="diretorio"><code class="r">

NAO_SRAG_VR <- SRAG_final %>%
  mutate(sem_def_srag = ifelse(is.na(caso_srag) | caso_srag != "1", 0, 1))


table(NAO_SRAG_VR$sem_def_srag)
#0         1 
#42606   82578


NAO_SRAG_VR <- SRAG_final %>%
  mutate(sem_def_srag = ifelse(is.na(caso_srag) | caso_srag != "1", 0, 1),
         casos_pos_sem_def = case_when(
           sem_def_srag == 0 & VIRUS_RESP %in% c("COVID-19", "INFLUENZA_A_H1N1", "METAPNEUMO", "OVR", 
                                                 "INFLUENZA_A_NAOSUB", "ADENOVIRUS", "SINCICIAL", "RINOVIRUS", 
                                                 "INFLUENZA_A_H3N2", "BOCAVIRUS", "INFLUENZA_B", "PARAINFLUENZA") ~ 1,  TRUE ~ 0))
table(NAO_SRAG_VR$ casos_pos_sem_def)

#0          1 
#111539   13645 

# Filtrar os dados para incluir apenas os casos positivos
casos_positivos <- NAO_SRAG_VR %>%
  filter(casos_pos_sem_def == 1)

# Contar a frequência de cada vírus na coluna VIRUS_RESP
frequencia_virus <- casos_positivos %>%
  group_by(VIRUS_RESP) %>%
  summarize(count = n()) %>%
  arrange(desc(count))

# Calcular o total de casos positivos
total_casos <- sum(frequencia_virus$count)

# Criar o gráfico de barras
grafico_casos_sem_def <- ggplot(frequencia_virus, aes(x = reorder(VIRUS_RESP, -count), y = count)) +
  geom_bar(stat = "identity", fill = "blue") +
  labs(title = paste("Distribuição dos Casos Positivos por Vírus sem definição de SRAG (N =", total_casos, ")"),
       x = "Vírus",
       y = "Número de Casos") +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))

print(grafico_casos_sem_def)


# Função para contar os valores 1, 0 e NA em uma coluna, com tratamento especial para a coluna EVOLUCAO
contar_valores <- function(coluna, coluna_nome) {
  if (coluna_nome == "EVOLUCAO") {
    tibble(
      Sim = sum(coluna == 2, na.rm = TRUE),
      Nao = sum(coluna != 2, na.rm = TRUE),
      NAs = sum(is.na(coluna))
    )
  } else {
    tibble(
      Sim = sum(coluna == 1, na.rm = TRUE),
      Nao = sum(coluna != 1, na.rm = TRUE),
      NAs = sum(is.na(coluna))
    ) }}



# Criar uma tabela com as contagens para cada variável
tabela_contagens <- tibble(
  Variavel = c("TOSSE", "GARGANTA", "HOSPITAL", "EVOLUCAO", "DISPNEIA", "DESC_RESP", "SATURACAO"),
  bind_rows(
    contar_valores(casos_positivos$TOSSE, "TOSSE"),
    contar_valores(casos_positivos$GARGANTA, "GARGANTA"),
    contar_valores(casos_positivos$HOSPITAL, "HOSPITAL"),
    contar_valores(casos_positivos$EVOLUCAO, "EVOLUCAO"),
    contar_valores(casos_positivos$DISPNEIA, "DISPNEIA"),
    contar_valores(casos_positivos$DESC_RESP, "DESC_RESP"),
    contar_valores(casos_positivos$SATURACAO, "SATURACAO")
  )
)


print(tabela_contagens)

# Exportar a tabela para um arquivo Excel
write_xlsx(tabela_contagens, "tabela_contagens.xlsx")

# Criar uma coluna combinando as variáveis TOSSE, GARGANTA, HOSPITAL, EVOLUCAO, DISPNEIA, DESC_RESP e SATURACAO
casos_positivos <- casos_positivos %>%
  mutate(combinacao = paste(
    ifelse(TOSSE == 1, "Sim", ifelse(TOSSE != 1, "Nao", "NA")),
    ifelse(GARGANTA == 1, "Sim", ifelse(GARGANTA != 1, "Nao", "NA")),
    ifelse(HOSPITAL == 1, "Sim", ifelse(HOSPITAL!= 1, "Nao", "NA")),
    ifelse(EVOLUCAO == 2, "Sim", ifelse(EVOLUCAO != 2, "Nao", "NA")),
    ifelse(DISPNEIA == 1, "Sim", ifelse(DISPNEIA != 1, "Nao", "NA")),
    ifelse(DESC_RESP == 1, "Sim", ifelse(DESC_RESP != 1, "Nao", "NA")),
    ifelse(SATURACAO == 1, "Sim", ifelse(SATURACAO != 1, "Nao", "NA")),
    sep = "_"
  ))

# Contar as combinações específicas
tabela_combinacoes <- casos_positivos %>%
  group_by(combinacao) %>%
  summarize(count = n()) %>%
  arrange(desc(count))

# Exportar a tabela de combinações para um arquivo Excel
write_xlsx(tabela_combinacoes, "tabela_combinacoes.xlsx")

# Ver a tabela resultante
print(tabela_combinacoes)

# Definir a condição "ideal"
condicao_ideal <- casos_positivos %>%
  filter((TOSSE == 1 | GARGANTA == 1) &
           (HOSPITAL == 1 | EVOLUCAO == 2) &
           (DISPNEIA == 1 | DESC_RESP == 1 | SATURACAO == 1))

# Exportar a tabela para um arquivo Excel
write_xlsx(condicao_ideal, "tabela_combinacoes_ideal.xlsx")

# Ver a tabela resultante
print(condicao_ideal)

</code></pre>
</div>


