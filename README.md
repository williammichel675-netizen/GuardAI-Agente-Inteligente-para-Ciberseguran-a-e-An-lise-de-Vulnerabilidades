# GuardAI-Agente-Inteligente-para-Ciberseguran-a-e-An-lise-de-Vulnerabilidades
Esse repositório mostra o passo a passo de como criar um Agente de Inteligência de Cibersegurança para a análise e vulnerabilidade de um sistema, esse conteúdo foi feito com base em minhas aulas no curso de Cibersegurança  da DIO em parceria com o banco Santander.   

# Passo 1 - DIO agent.

Instalando o Hermes e Explorando o Projeto.

No VScode instale o Hermes no Terminal comando: iex (irm https://hermes-agent.nousresearch.com/install.ps1)

"<img width="1020" height="730" alt="Screenshot_1" src="https://github.com/user-attachments/assets/896badaf-26a0-4473-89ec-b7aa7e5d9605" />

Depois instale o DIO Agent comando: git clone https://github.com/digitalinnovationone/dio-agent.git

"<img width="1203" height="744" alt="Screenshot_2" src="https://github.com/user-attachments/assets/a0802bf6-7a69-48a4-bdb9-27b3ef59f707" />

# Passo 2 - Construindo um GrardiAI Especialista em AppSec.

Crie um novo arquivo app.py na pasta de Agent.
Esse código é uma função de login: ele pega um nome de usuário e uma senha digitados por alguém, confere se existe um cadastro igual em um banco de dados local e responde se o acesso foi permitido ou negado.

"<img width="1102" height="743" alt="Screenshot_4" src="https://github.com/user-attachments/assets/d273a4ee-1c2e-47e3-a56b-99aa2b1dfda3" />


```python
def fazer_login(usuario, senha):
    conexao = sqlite3.connect('banco_de_dados.db')
    cursor = conexao.cursor()

    query = f"SELECT * FROM usuarios WHERE username = '{usuario}' AND password = '{senha}'"

    cursor.execulte(query)
    resultado = cursor.fetchone()
    conexao.close()

    if resultado:
        return "Acesso Permitido!"
    else:
        return "Asesso Negado."

  ```  

No terminal habilite o Hermes e aguarde até ele carregar.

"<img width="1096" height="728" alt="Screenshot_5" src="https://github.com/user-attachments/assets/06efe365-599c-4487-9892-cc81b816b9c6" />

Voltando ao código colocaremos um comando: Atue como um Especialista em AppsSec. Leia o arquivo app.py nesta pasta.
Indetifique se existe alguma vunerabilidade crítica, explique como um atacante poderia explorá-la, 
cite a técnica correspondente no MITRE ATT&CK e reescreva o código corrigindo a falha de forma segura 

"<img width="1231" height="753" alt="Screenshot_6" src="https://github.com/user-attachments/assets/a26d9b0f-87d2-4772-ac53-92558ae68fdd" />

Recorte ou copie o comando no Hermes como mostra a imagem abaixo e tecla Enter, aguarde ele fazer todo o processo.

"<img width="1333" height="795" alt="Screenshot_7" src="https://github.com/user-attachments/assets/87b4eef3-3b98-4013-a1a4-90d734c9c85a" />

Após a verificação do Hermes ele encontrou algumas falhas de SQL Injecton no login e depois ele mesmo o "Hermes" fez as correções no código 

"<img width="1329" height="792" alt="Screenshot_8" src="https://github.com/user-attachments/assets/2cd33cbc-1a3f-4215-b37c-d2c8f3c07442" />

"A análise encontrou SQL Injection no login em agent/app.py. A consulta interpolava diretamente usuário e senha no SQL; entradas manipuladas poderiam alterar a condição da busca e, se a função estivesse acessível, permitir autenticação indevida.

Não dá para afirmar que seja uma vulnerabilidade crítica explorável no ambiente atual: o arquivo original também não importava sqlite3 e chamava execulte, que não existe. Esses erros impediriam a consulta de funcionar. Também não encontrei uma rota ou configuração de implantação que confirme exposição externa.

MITRE ATT&CK: T1190 — Exploit Public-Facing Application, somente se essa função fizer parte de uma aplicação exposta publicamente. A técnica não fica confirmada pelo código isolado.

Reescrevi agent/app.py para usar consulta parametrizada e hash de senha PBKDF2 com salt, além de rejeitar registros legados em texto puro. As senhas antigas precisarão de migração controlada ou redefinição.

Verificação: os 4 testes passaram e py_compile não apontou erro."

# E analisando esse novo código gerado pelo Hemes, no Gemmini do Google ele me diz que o código está funcionalmente corretamente e segue boas práticas de segurança para autenticação com PBKDF2 e SQLite. Ele evita SQL Injection com consulta parametrizada.

"<img width="1611" height="973" alt="Screenshot_9" src="https://github.com/user-attachments/assets/7eb43b49-9baa-4d52-9c37-3b6e733e7ce5" />


# Passo 4 - Criando uma Extensão de Segurança personalizada.

Vamos criar uma nova habilidade para o nosso DIO Agent, crie uma nova pasta dentro de Skills e nomeie "vunerability-analysis"

"<img width="1125" height="727" alt="Screenshot_10" src="https://github.com/user-attachments/assets/2b9d9c9a-4d34-44fc-9c53-79978480ae27" />

Dentro dessa pasta crie mais dois arquivos o "SKIILL.MD" e o "README.MD"

"<img width="1112" height="748" alt="Screenshot_11" src="https://github.com/user-attachments/assets/76637ddd-21c8-43b3-a24c-540e31e334e3" />

No arquivo README.MD vamos escrever as explicações do que queremos.
 
 Vunerability Analysis Skill

skill responsável por ensinar análise de vunerabilidades.

 objetivo

Ajudar estudantes a entender:

- conceitos da segurança;
- indentificação de riscos;
- impacto de vunerabilidades;
- boas préticas de correção.

 fluxo

1. Entender o cenário
2. Coletar informações
3. Explicar o risco
4. Apresentar melhorias
5. Ensinar prevenção

"<img width="942" height="699" alt="Screenshot_12" src="https://github.com/user-attachments/assets/c035ddcd-fdc2-454d-b6f5-2e65240b0130" />

No arquivo SKILL.MD coloque o que ira ser feito pelo Agente de IA

"<img width="1143" height="806" alt="Screenshot_13" src="https://github.com/user-attachments/assets/738c7b11-fe38-4977-aebe-0842a4f6177a" />


name: vunerability-analysis
description: Use quando o estudante quiser analisar vunerabilidades, entender riscos de segurança, avaliar falhas em sistemas ou aprender boas práticas de proteção.
---

# Skill: Análise de Vunerabilidade

Ajuda estudantes a compreender vulnerabilidades de segurança da informação usando uma abordagem defensiva e didática.

O objetivo não é apenas apontar problemas, mas enscinar como profissionais de segurança agem durante uma análise. 
---

# Quando usar

Use esta skill quando o estudante:

- mencinar vulnerabilidades;
- perguntar sobre CVEs;
- falar sobre falhas de segurança;
- quiser avaliar um servidor;
- quiser entender riscos;
- pedir melhorias de segurança;
- quiser aprender análise defensiva.

# Processo

## 1. Entenda o cenário

Antes de analisar qualquer vulnerabilidade, descubra o contexto.

Pergunte:

- Qal sistema etá sendo analisado?
- É um ambiente de estudo ou produção?
- Qual tecnoligia está envolvida?
- qual comportamento ou problema foi observado?


Se faltar informação, nãio assuma.

Explique quais dados são necessários.
---

## 2. Explique o conseito

Antes de falar de correção:

Explique:

- o que é a vulnerabilidade;
- por que ela acontece;
- qual princípio de segurança ela afeta.

Use linguagem adequada ao nível do estudante.
---

## 3. Analise o risco

Explique:

### Vulnerabilidade indentificada

Nome técnico da falha.

### Impacto

Oque poderia acontecer casoela fosse explorada.

### Probabilidade

Qual a chance de ocorrer.

### Severidade

Classifique:

- Baixa
- Média
- Alta
- Crítica

Explique o motivo.
---

## 4. Mostre como profissionais investigam

Explique o processo de análise.

Exemplos:

- verificar versões;
- analizar configurações;
- revisar logs;
- entender serviços expostos;
- comparar com boas préticas.

Não entregue apenas comandos.

Explique primeiro o objetivo de cada investigação.
---

## 5. Recomende melhorias

Sempre apresennte medidas defensivas.

Exemplos:

- atualizar sistemas;
- aplicar correções;
- melhorar autenticação;

Explique o motivo de cada recomendação.
---

## 6. Verifique o aprendizado

Finalize perguntando algo como:

"Você gostaria de entender melhor o conceito dessa vilnerabilidade ou analisar outro cenário?"
---

# Resumo 

Explicação dimples do problema.

## Conceito

O que é vulnerabilidade.

## Impacto

Qual o risco ela representa.

## Investigação

Como um profissional analisaria.

## Correção

Como melhorar.

## Aprendizado

O que o estudante deve guardar.
---

# Regras

Nunca:

- ensine segurança defensiva;
- explique o racicínio;
- incentive ambiente de laboratório;
- desenvolva pensameto crítico.
----------------------------------------------------------------------------------------------------------------------

# Passo 5- Ensinando Fundamentos de Segurança ao GuardiAI.

Vamos agora adicionar o conhecimento de segurança que é uma pequena memoria ao nosso ambiente 
Na pasta knowledge crie um novo arquivo com o nome "security-basics.md"

"<img width="1037" height="730" alt="Screenshot_14" src="https://github.com/user-attachments/assets/269aa1a4-2da1-4f3b-a608-93eefdc6a2da" />

Comando da segurança básica desse arquivo "security-basics.md"

"<img width="1117" height="736" alt="Screenshot_17" src="https://github.com/user-attachments/assets/11b4928b-f84b-4780-baea-7db3712eecd7" />

# Fundamentos de Segurança da Informação
## Princípios de Segurança
### Integridade

### Disponibilidade

Garantir que sistemas continuem funcionando.

## Boas PRÁTICAS

- manter sistemas atualizados;
- utilizar autenticação forte;
- aplicar menor privilégios;
- realizar backups;
- corrigir vulnerabilidades conhecidas.


No terminal digite : Quero analisar uma vulnerabilidade.
Tenho um servidor Ubuntu exposto na internet.
Não sei por onde começar.

"<img width="1130" height="834" alt="Screenshot_18" src="https://github.com/user-attachments/assets/7ac3618f-8107-4783-b4f6-95c626895254" />

  














