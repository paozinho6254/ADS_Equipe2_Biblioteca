# Unibiblio - Sistema de Gestão de Biblioteca---

## se

## Tecnologias Utilizadas

- **Linguagem:** [Java 17](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html)
- **Framework:** [Spring Boot](https://spring.io/projects/spring-boot)
  - Spring Web MVC
  - Spring Data JPA / Hibernate
- **Banco de Dados:** [H2 Database](https://www.h2database.com/) (em memória para desenvolvimento e testes)
- **Gerenciador de Dependências:** [Apache Maven](https://maven.apache.org/)

---

## Estrutura do Projeto

O código-fonte está estruturado sob o pacote base `com.unibiblio`:

```text
src/main/java/com/unibiblio/
├── UnibiblioApplication.java          # Classe principal de inicialização da aplicação Spring Boot
├── application/
│   ├── controller/
│   │   └── ControladorCadastroLivro.java  # Controladores e pontos de entrada de operações
│   └── service/
│       └── NotificacaoWorker.java         # Serviços de negócio e rotinas de notificação
├── domain/
│   ├── enums/
│   │   ├── ModalidadePagamento.java       # Formas de pagamento aceitas
│   │   ├── StatusEmprestimo.java          # Estados de um empréstimo (ativo, devolvido, etc.)
│   │   ├── StatusExemplar.java            # Disponibilidade física do exemplar
│   │   ├── StatusMulta.java               # Estados de multa (pendente, paga, etc.)
│   │   └── StatusReserva.java             # Estados do ciclo de vida de uma reserva
│   ├── model/
│   │   ├── Administrador.java             # Perfil administrativo do sistema
│   │   ├── Aluno.java                     # Perfil de aluno / usuário leitor
│   │   ├── Bibliotecario.java             # Perfil operacional da biblioteca
│   │   ├── Emprestimo.java                # Registro e regras de empréstimo
│   │   ├── Exemplar.java                  # Unidade física associada a um título
│   │   ├── Livro.java                     # Catálogo bibliográfico
│   │   ├── Multa.java                     # Cobrança gerada por atraso
│   │   ├── Pagamento.java                 # Quitação de multas e taxas
│   │   ├── Reserva.java                   # Agendamento de títulos emprestados
│   │   └── Usuario.java                   # Classe base abstrata para usuários
│   └── printing/
│       └── ComprovanteDevolucao.java      # Geração e emissão de comprovantes de devolução
└── repository/
    ├── IEmprestimoRepository.java         # Acesso a dados para empréstimos
    └── ILivroRepository.java              # Acesso a dados para livros
```

---

## Funcionalidades Principais

- **Gestão de Usuários:** Cadastro e diferenciação de permissões para Alunos, Bibliotecários e Administradores.
- **Controle de Acervo:** Cadastro de obras (`Livro`) e seus respectivos exemplares físicos (`Exemplar`).
- **Circulação:**
  - Realização de empréstimos e controle de devoluções.
  - Emissão de comprovante de devolução (`ComprovanteDevolucao`).
  - Fila de reservas para livros indisponíveis no momento.
- **Financeiro / Sanções:**
  - Aplicação automática de multas por atraso na devolução.
  - Registro de pagamentos de multas em diferentes modalidades.
- **Notificações:** Rotina assíncrona (`NotificacaoWorker`) para avisos de vencimento e disponibilidade de reservas.

---

## Como Executar o Projeto

### Pré-requisitos

- **Java JDK 17 ou 21** instalado e configurado no `PATH`
- **Git**

### Passo a passo

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/ADS-Equipe2/ADS_Equipe2_Biblioteca.git
   cd ADS_Equipe2_Biblioteca
   ```

2. **Execute a aplicação com o Maven Wrapper:**
   - **Linux / macOS:**
     ```bash
     ./mvnw spring-boot:run
     ```
   - **Windows:**
     ```cmd
     mvnw.cmd spring-boot:run
     ```

3. **Executar os testes unitários:**
   ```bash
   ./mvnw test
   ```

---

## Acesso ao Banco de Dados (Ainda temporário)

Com a aplicação em execução, o console do banco H2 pode ser acessado pelo navegador:

- **URL:** [http://localhost:8080/h2-console](http://localhost:8080/h2-console)
- **JDBC URL:** `jdbc:h2:mem:testdb`
- **Driver Class:** `org.h2.Driver`
- **Usuário:** `sa`
- **Senha:** *(deixe em branco)*


