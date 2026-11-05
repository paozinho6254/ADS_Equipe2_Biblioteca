# Unibiblio - Sistema de Gestão de Biblioteca---

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
- *(Opcional)* **Maven**: **Não é necessário ter o Maven instalado na máquina.** O projeto já inclui o **Maven Wrapper**, que baixa e configura a versão necessária do Maven automaticamente.

### Passo a passo

1. **Verificar se o Java está instalado:**
   Abra o terminal (ou Prompt de Comando/PowerShell) e verifique se o Java está acessível:
   ```bash
   java -version
   ```
   > Deve exibir uma versão do Java 17 ou superior.

2. **Clonar o repositório:**
   Faça o clone do projeto para a sua máquina e entre na pasta:
   ```bash
   git clone https://github.com/ADS-Equipe2/ADS_Equipe2_Biblioteca.git
   cd ADS_Equipe2_Biblioteca
   ```

3. **Executar a aplicação com o Maven Wrapper (sem precisar instalar o Maven):**
   Como o Maven Wrapper (`mvnw` / `mvnw.cmd`) já está incluso na raiz do projeto, você não precisa baixar ou configurar o Maven manualmente no sistema operacional. Na primeira vez que for executado, o script fará o download automático da versão correta do Maven e de todas as bibliotecas necessárias.

   - **Linux / macOS:**
     *(Se necessário, conceda permissão de execução ao script no primeiro uso)*
     ```bash
     chmod +x mvnw
     ./mvnw spring-boot:run
     ```

   - **Windows:**
     - No **Prompt de Comando (CMD)**:
       ```cmd
       mvnw.cmd spring-boot:run
       ```
     - No **PowerShell**:
       ```powershell
       .\mvnw.cmd spring-boot:run
       ```

   > **Dica na primeira inicialização:** O primeiro download das dependências e do Maven pode levar alguns minutos. Quando aparecer no terminal a mensagem indicando que a aplicação iniciou (ex.: `Started UnibiblioApplication`), o sistema estará ativo e ouvindo na porta `8080`.

4. **Executar os testes da aplicação (opcional):**
   Para rodar a bateria de testes unitários sem precisar do Maven instalado:
   - **Linux / macOS:**
     ```bash
     ./mvnw test
     ```
   - **Windows:**
     ```cmd
     mvnw.cmd test
     ```

---

## Como editar o projeto

## NUNCA DE COMMIT'S NA MAIN

---

## Acesso ao Banco de Dados (Ainda temporário)

Com a aplicação em execução, o console do banco H2 pode ser acessado pelo navegador:

- **URL:** [http://localhost:8080/h2-console](http://localhost:8080/h2-console)
- **JDBC URL:** `jdbc:h2:mem:testdb`
- **Driver Class:** `org.h2.Driver`
- **Usuário:** `sa`
- **Senha:** *(deixe em branco)*


