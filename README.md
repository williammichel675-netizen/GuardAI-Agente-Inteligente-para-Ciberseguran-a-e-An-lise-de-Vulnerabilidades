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
import sqlite3


def fazer_login(usuario, senha):
    conexao = sqlite3.connect("banco_de_dados.db")
    cursor = conexao.cursor()

    query = "SELECT * FROM usuarios WHERE username = ? AND password = ?"
    cursor.execute(query, (usuario, senha))
    resultado = cursor.fetchone()

    conexao.close()

    if resultado:
        return "Acesso Permitido!"
    return "Acesso Negado."
``` 
No terminal habilite o Hermes e aguarde até ele carregar.

"<img width="1096" height="728" alt="Screenshot_5" src="https://github.com/user-attachments/assets/06efe365-599c-4487-9892-cc81b816b9c6" />

Voltando ao código colocaremos um comando: Atue como um Especialista em AppsSec. Leia o arquivo app.py nesta pasta.
Indetifique se existe alguma vunerabilidade crítica, explique como um atacante poderia explorá-la, 
cite a técnica correspondente no MITRE ATT&CK e reescreva o código corrigindo a falha de forma segura 

"<img width="1231" height="753" alt="Screenshot_6" src="https://github.com/user-attachments/assets/a26d9b0f-87d2-4772-ac53-92558ae68fdd" />



