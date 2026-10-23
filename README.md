# Oficina SAEP

Aplicação web para apoiar a gestão de uma oficina mecânica. O sistema reúne cadastro de clientes e veículos, agendamento de serviços e um painel com indicadores básicos.

> Projeto educacional relacionado ao SAEP/SENAI. A aplicação depende de um banco MySQL preparado previamente.

## Funcionalidades

- Autenticação de usuários com sessão e expiração configurada para 15 minutos.
- Painel com totais de clientes, veículos e agendamentos, além dos próximos serviços.
- Cadastro, edição, pesquisa e remoção de clientes.
- Cadastro, edição e remoção de veículos, vinculados a um cliente.
- Cadastro, reagendamento e remoção de serviços.
- Interface em português, desenvolvida com templates HTML, CSS e JavaScript.

## Tecnologias

- Python e Flask
- MySQL e `mysql-connector-python`
- `bcrypt`
- HTML, CSS e JavaScript

## Estrutura

O código executável da aplicação fica em `arquivo_oficina/projetos/oficina`:

```text
.
├── README.md
└── arquivo_oficina/
    ├── README.md
    └── projetos/
        └── oficina/
            ├── app.py
            ├── autenticacao.py
            ├── banco.py
            ├── clientes.py
            ├── veiculos.py
            ├── agendamento.py
            ├── rotas.py
            ├── templates/
            ├── static/
            └── guia_passo_a_passo_aula.md
```

O guia passo a passo contém a modelagem SQL e instruções adicionais de desenvolvimento. Atualmente, o repositório não inclui um `requirements.txt` nem um arquivo `.sql` separado.

## Requisitos

- Python 3.10 ou superior
- MySQL em execução
- Banco de dados e tabelas criados conforme a seção **Fase 2: Banco de Dados Relacional** do arquivo `arquivo_oficina/projetos/oficina/guia_passo_a_passo_aula.md`

## Instalação e execução

Clone o repositório e entre na pasta da aplicação:

```bash
git clone https://github.com/mathiasfelippe/oficina_saep.git
cd oficina_saep/arquivo_oficina/projetos/oficina
```

Crie e ative um ambiente virtual:

```bash
python -m venv .venv

# Linux ou macOS
source .venv/bin/activate

# Windows PowerShell
.venv\Scripts\Activate.ps1
```

Instale as dependências usadas no projeto e indicadas no guia:

```bash
python -m pip install Flask==3.0.3 mysql-connector-python==8.4.0 bcrypt==4.1.3 Werkzeug==3.0.3
```

Configure o acesso ao MySQL por variáveis de ambiente. Substitua os valores pelos dados do seu ambiente:

```bash
# Linux ou macOS
export DB_HOST=localhost
export DB_PORT=3306
export DB_USER=seu_usuario
export DB_PASSWORD='sua_senha'
export DB_NAME=saep_db
export SECRET_KEY='gere-uma-chave-aleatoria-para-sua-sessao'
```

No Windows PowerShell, use `$env:DB_HOST="localhost"` e atribuições equivalentes para as demais variáveis.

Depois de criar o banco e as tabelas conforme o guia, inicie o servidor:

```bash
python app.py
```

Acesse [http://127.0.0.1:5000](http://127.0.0.1:5000). O aplicativo redireciona para a tela de login.

## Configuração do banco

O módulo `banco.py` lê `DB_HOST`, `DB_PORT`, `DB_USER`, `DB_PASSWORD` e `DB_NAME`. Se as variáveis não forem definidas, ele utiliza valores padrão locais; prefira configurar suas próprias variáveis e não use credenciais de desenvolvimento em ambientes compartilhados.

Para preparar as tabelas e, se necessário, os dados de exemplo, consulte e execute no MySQL o SQL documentado na **Fase 2** do guia. O esquema inclui as tabelas `usuarios`, `clientes`, `veiculos` e `agendamentos`.

## Observação sobre dados pessoais

O código gera um hash Bcrypt do CPF, mas também grava o CPF formatado na coluna `clientes.cpf` e o exibe na interface. Portanto, o hash não equivale à criptografia do dado armazenado. Antes de utilizar dados reais ou disponibilizar o sistema publicamente, revise o tratamento de dados pessoais, as credenciais padrão e a chave de sessão.

## Licença

Nenhuma licença de código foi identificada no repositório. Consulte o responsável pelo projeto antes de reutilizar ou distribuir o código.
