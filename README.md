<div align="center">

<img src="assets/imagens/logo.png" alt="Logo da Velozzi Locadora" width="220">

# Velozzi Locadora

**Sistema desktop de locação de veículos feito em Java (Swing) com banco de dados PostgreSQL**

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Swing](https://img.shields.io/badge/Java_Swing-1572B6?style=for-the-badge)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)

</div>

---

## 📚 Sobre o projeto

Projeto da disciplina de **Projeto Integrador Computação II**, do curso de **Análise e Desenvolvimento de Sistemas**. A proposta era desenvolver um sistema completo integrando programação e banco de dados, e nosso grupo criou a **Velozzi Locadora**, um sistema para gerenciar veículos, clientes, locações e faturamento de uma locadora.

## ✨ Funcionalidades

| Recurso | Descrição |
|---|---|
| 🔐 Login seguro | Acesso por usuário e senha, com senha armazenada em hash (PBKDF2) |
| 📊 Dashboard | Visão geral com total de veículos, clientes, locações e faturamento do mês |
| 🚘 Veículos | Cadastro, edição, exclusão e listagem da frota (placa, modelo, marca e cor) |
| 👤 Clientes | Cadastro, edição, exclusão e listagem; impede excluir cliente que já tem locação |
| 📝 Locações | Registra a locação, valida se o veículo está disponível e registra a devolução |
| 💰 Faturamento | Gera o faturamento junto com a locação, calcula as diárias e registra pagamento ou cancelamento |
| 💳 Formas de pagamento | PIX, dinheiro, cartão de crédito e cartão de débito |
| 📈 Relatórios | Locações por modelo e duração das locações |
| ⚠️ Validações | Tratamento de erros e regras de negócio com mensagens claras para o usuário |

## 🛠️ Tecnologias

| Tecnologia | Uso |
|---|---|
| **Java 25** | Linguagem principal e lógica do sistema |
| **Java Swing** | Interface gráfica desktop |
| **PostgreSQL** | Banco de dados relacional |
| **JDBC (`postgresql-42.7.14.jar`)** | Conexão entre o Java e o PostgreSQL |
| **Git e GitHub** | Versionamento e trabalho em equipe |

## 🏗️ Arquitetura

O projeto segue o padrão **MVC** com camada de acesso a dados (**DAO**):

| Camada | Pacote | Responsabilidade |
|---|---|---|
| **Model** | `model` | Classes de domínio (`Cliente`, `Veiculo`, `Locacao`, `Faturamento`, `Usuario`) |
| **View** | `view` | Telas em Swing (login, dashboard, veículos, clientes, locações, faturamento e relatórios) |
| **Controller** | `controller` | Regras de negócio e validações |
| **DAO** | `dao` | Comandos SQL e acesso ao banco |
| **Config** | `config` | Conexão com o PostgreSQL |

## 📋 Pré-requisitos

- [JDK 25](https://jdk.java.net/25/) instalado e configurado no `PATH`
- [PostgreSQL](https://www.postgresql.org/download/) instalado e em execução
- Driver `postgresql-42.7.14.jar` (já incluído na pasta `lib/`)

## 🚀 Como rodar localmente

**1. Clone o repositório**

```bash
git clone https://github.com/WalissonP/velozzi-locadora.git
cd velozzi-locadora
```

**2. Crie o banco de dados**

```sql
CREATE DATABASE locadora;
```

**3. Crie as tabelas e insira os dados iniciais**

Conectado ao banco `locadora`, execute os scripts nesta ordem:

1. `sql/criar_tabelas.sql`
2. `sql/inserir_dados.sql`

**4. Configure a conexão**

Se o seu PostgreSQL usar outro usuário ou senha, ajuste em `src/com/locadora/config/DatabaseConnection.java`:

```java
private static final String URL = "jdbc:postgresql://localhost:5432/locadora";
private static final String USER = "postgres";
private static final String PASSWORD = "root";
```

**5. Compile e execute**

Rode os comandos a partir da **pasta raiz do projeto**, pois o sistema carrega as imagens de `assets/imagens`.

```bash
# Linux / macOS
javac -cp lib/postgresql-42.7.14.jar -d out $(find src -name "*.java")
java -cp "out:lib/postgresql-42.7.14.jar" com.locadora.Main
```

```powershell
# Windows (PowerShell)
javac -cp lib/postgresql-42.7.14.jar -d out (Get-ChildItem -Recurse src -Filter *.java).FullName
java -cp "out;lib/postgresql-42.7.14.jar" com.locadora.Main
```

> Se preferir uma IDE (VS Code, IntelliJ, Eclipse ou NetBeans), basta abrir a pasta, garantir que o `.jar` da pasta `lib/` está nas bibliotecas e executar a classe `com.locadora.Main`.

## 🔑 Acesso ao sistema

O script `inserir_dados.sql` cria um usuário administrador para o primeiro acesso:

| Usuário | Senha |
|---|---|
| `admin` | `Admin@123` |

## 🗄️ Banco de dados

| Tabela | Descrição |
|---|---|
| `usuarios` | Usuários do sistema (senha em hash) |
| `cliente` | Clientes da locadora |
| `veiculos` | Frota de veículos |
| `locacao` | Locações, ligadas a um cliente e a um veículo (status `LOCADO` ou `DISPONIVEL`) |
| `faturamento` | Cobrança de cada locação (diárias, valor total, forma e status do pagamento) |

## 📁 Estrutura do projeto

```text
velozzi-locadora/
├── assets/
│   └── imagens/
│       ├── logo.png
│       └── ...
├── lib/
│   └── postgresql-42.7.14.jar
├── sql/
│   ├── criar_tabelas.sql
│   └── inserir_dados.sql
├── src/
│   └── com/locadora/
│       ├── config/
│       ├── controller/
│       ├── dao/
│       ├── model/
│       ├── relatorioDados/
│       ├── view/
│       └── Main.java
├── .gitignore
└── README.md
```

## 🧠 Conceitos praticados

- Programação orientada a objetos em Java
- Padrão MVC e camada DAO
- Interface gráfica com Java Swing
- Conexão com banco de dados via JDBC
- Modelagem e criação de banco de dados relacional (chaves estrangeiras e `CHECK`)
- Operações CRUD (criar, ler, atualizar e excluir)
- Tratamento de exceções e regras de negócio
- Hash de senha com PBKDF2
- Trabalho em equipe e versionamento com Git

## 👥 Equipe

-   [Bryan Monteiro](https://github.com/anonimo172006)
-   [Cesar Peixoto](https://github.com/Ceasa20)
-   [Davi Pitangui](https://github.com/davzhin)
-   [Gabryel Modesto](https://github.com/Gabryel-Modesto)
-   [Nathália Lima](https://github.com/natyylimaf)
-   [Walisson Pastori](https://github.com/WalissonP)

---
