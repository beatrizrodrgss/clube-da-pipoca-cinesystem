# Plano de Testes - Tela de Cadastro do Clube da Pipoca [Cinesystem]

## Introdução
Este repositório contém o plano de testes detalhado para o Clube da Pipoca Cinesystem, focado na tela de cadastro de novos usuários. O objetivo é garantir que todas as funcionalidades sejam validadas, proporcionando uma experiência segura, intuitiva e eficiente para os usuários.

### 1. Identificação do Plano de Teste
- Nome do Projeto: Clube da Pipoca Cinesystem
- Data: 25/11/2024
- Responsável: Beatriz Rodrigues
- Versão do Documento: 1.0

### 2. Descrição da Tela
A tela de cadastro possui os seguintes campos:

- Nome Completo
- Data de Nascimento (formato dd/mm/aaaa)
- CPF (formato 999.999.999-99)
- E-mail
- Cinema (Select)
- Celular (formato (99) 99999-9999)
- Senha 
- Confirmação de Senha
- Checkboxes: 
    - Consentimento de marketing (opcional)
    - Aceite dos Termos e Condições (obrigatório)

### 3. Escopo do Teste
Verificar que:

- Os campos sejam validados adequadamente.
- O cadastro seja realizado com dados válidos e exiba mensagens claras em casos de erro.
- Todos os campos obrigatórios sejam preenchidos antes de enviar o formulário.
- Consentimentos e o aceite dos termos sejam corretamente registrados no sistema.
- A interface seja responsiva e funcional em diferentes dispositivos e navegadores.

### 4. Tipos de Teste
- Funcionalidade: Validar campos, envio e comportamento esperado.
- UI/UX: Garantir clareza e usabilidade da interface.
- Segurança: Testar proteção de dados e entrada maliciosa.
- Compatibilidade: Verificar comportamento em diferentes dispositivos e navegadores.

### 5. Ferramentas Utilizadas
#### Automação de Testes:
- Cypress: Testes funcionais e E2E.
- Selenium: Testes cross-browser e UI.
- Postman: Testes de API (se aplicável).
#### Gerenciamento e Relatórios:
- JIRA/TestRail: Gestão de casos e planos de teste.
#### Testes de Performance:
- K6: Simulação de carga para endpoints de backend (se o cadastro envolver APIs).
#### Validação Manual:
- Planilhas para controle inicial ou ferramentas simples como Google Sheets.

### 6. Casos de Teste
### Funcionalidade
| **ID**  | **Cenário**                            | **Passos**                                                                                 | **Resultado Esperado**                         |
|---------|----------------------------------------|--------------------------------------------------------------------------------------------|-----------------------------------------------|
| CT01    | Cadastro com todos os campos válidos  | 1. Preencher todos os campos corretamente<br>2. Aceitar os termos<br>3. Clicar "Cadastrar" | Cadastro realizado com sucesso               |
| CT02    | Campo "Nome" vazio                    | 1. Deixar o campo "Nome" vazio<br>2. Preencher os demais campos<br>3. Clicar "Cadastrar"   | Mensagem: "Preencha seu nome completo"        |
| CT03    | Data de nascimento inválida           | 1. Inserir "31/02/2020" no campo<br>2. Preencher os demais campos<br>3. Clicar "Cadastrar" | Mensagem: "Insira uma data de nascimento válida" |
| CT04    | CPF com formato errado                | 1. Inserir "12345678900" no campo CPF<br>2. Preencher os demais campos<br>3. Clicar "Cadastrar" | Mensagem: "CPF inválido. Formato esperado: 999.999.999-99" |
| CT05    | Seleção de cinema não preenchida      | 1. Deixar o campo "Cinema" como "Selecione"<br>2. Preencher os demais campos<br>3. Clicar "Cadastrar" | Mensagem: "Selecione um cinema preferido"    |
| CT06    | E-mail em formato inválido            | 1. Inserir "usuario.com.br" no campo E-mail<br>2. Preencher os demais campos<br>3. Clicar "Cadastrar" | Mensagem: "Insira um e-mail válido"          |
| CT07    | Campo "Celular" vazio                 | 1. Deixar o campo "Celular" vazio<br>2. Preencher os demais campos<br>3. Clicar "Cadastrar" | Mensagem: "Insira seu número de celular"     |
| CT08    | Senhas não coincidem                  | 1. Inserir senhas diferentes nos campos "Senha" e "Confirmação"<br>2. Preencher os demais campos<br>3. Clicar "Cadastrar" | Mensagem: "As senhas não coincidem"          |
| CT09    | Aceite dos Termos não marcado         | 1. Preencher todos os campos corretamente<br>2. Não marcar o checkbox "Aceite dos Termos"<br>3. Clicar "Cadastrar" | Mensagem: "É necessário aceitar os termos para prosseguir" |

---

### Segurança
| **ID**  | **Cenário**                           | **Passos**                                                                                 | **Resultado Esperado**                         |
|---------|---------------------------------------|--------------------------------------------------------------------------------------------|-----------------------------------------------|
| CT10    | SQL Injection em qualquer campo       | 1. Inserir `' OR 1=1;--` em qualquer campo do formulário<br>2. Clicar "Cadastrar"          | Sistema rejeita a entrada e exibe mensagem genérica |
| CT11    | CPF duplicado                         | 1. Tentar cadastrar um CPF já existente no sistema<br>2. Clicar "Cadastrar"               | Mensagem: "CPF já cadastrado"                 |

---

### UI/UX
| **ID**  | **Cenário**                           | **Passos**                                                                                 | **Resultado Esperado**                         |
|---------|---------------------------------------|--------------------------------------------------------------------------------------------|-----------------------------------------------|
| CT12    | Mensagens de erro claras              | 1. Inserir dados inválidos em múltiplos campos<br>2. Clicar "Cadastrar"                    | Mensagens específicas exibidas para cada erro |
| CT13    | Responsividade em dispositivos móveis | 1. Acessar a tela de cadastro em um smartphone<br>2. Validar layout e funcionalidade       | Layout adaptado sem falhas de funcionalidade  |

---

### 7. Estrutura para BDD e TDD
#### Exemplo de Cenário BDD (Gherkin)
```gherkin
Feature: Cadastro de novos usuários
  Scenario: Cadastro com todos os campos preenchidos corretamente
    Given Estou na página de cadastro
    When Preencho "Nome" com "João Silva"
    And Preencho "Data de Nascimento" com "15/08/1990"
    And Preencho "CPF" com "123.456.789-00"
    And Preencho "E-mail" com "joao.silva@example.com"
    And Seleciono "Cinema" com "Shopping A"
    And Preencho "Celular" com "(11) 98765-4321"
    And Preencho "Senha" com "SenhaForte123"
    And Preencho "Confirmação" com "SenhaForte123"
    And Marco o checkbox "Aceite dos Termos"
    And Clico no botão "Cadastrar"
    Then Vejo a mensagem "Cadastro realizado com sucesso"
```
#### Exemplo de Teste TDD com Cypress
```javascript
describe('Cadastro de Usuário', () => {
  it('Deve exibir erro ao tentar cadastrar sem aceitar os termos', () => {
    cy.visit('/cadastro');
    cy.get('#nome').type('João Silva');
    cy.get('#dataNascimento').type('15/08/1990');
    cy.get('#cpf').type('123.456.789-00');
    cy.get('#email').type('joao.silva@example.com');
    cy.get('#cinema').select('Shopping A');
    cy.get('#celular').type('(11) 98765-4321');
    cy.get('#senha').type('SenhaForte123');
    cy.get('#confirmarSenha').type('SenhaForte123');
    // Não marcar o checkbox dos termos
    cy.get('#cadastrar').click();
    cy.get('.mensagem-erro').should('contain', 'É necessário aceitar os termos para prosseguir');
  });
});
```

### 8. Conclusão

- Com a execução deste plano de testes, garantiremos que a tela de cadastro atende aos padrões de qualidade esperados, proporcionando segurança e usabilidade aos usuários.

- Após a conclusão dos testes, os resultados serão analisados para priorização de correções e melhorias antes da liberação para produção.

- Certificar-se de que todos os casos foram executados, erros documentados e re-testes realizados.

- Responsáveis pela Execução 
   - QA Beatriz Rodrigues será responsável por realizar a execução dos casos e validação dos resultados.

- Referências / Anexos
   - Site Clube da Pipoca Cinesystem: https://clubedapipoca.cinesystem.com.br/
   - Tela de Cadastros: https://clubedapipoca.cinesystem.com.br/cadastro/
