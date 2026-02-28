Sistema de Clínica Veterinária
Este projeto tem como objetivo desenvolver o modelo de dados para uma clínica veterinária de pequeno porte.

O sistema foi modelado para gerenciar:
- Cadastro de pessoas (clientes e funcionários)
- Cadastro de animais
- Registro de atendimentos
- Controle de produtos
- Controle de serviços
- Registro de pagamentos

Aqui estão definidos:
- Entidades do sistema
- Chaves primárias (PK)
- Chaves estrangeiras (FK)
- Relacionamentos (1:1, 1:N e N:N)
- Tabelas associativas
- Diagrama ER

```mermaid
---
config:
  theme: neo-dark
---
erDiagram
    Pessoa {
        int ID_Pessoa PK
        string Nome
        string CPF UK
        string Telefone
    }
    Cliente {
        int ID_Cliente PK
        int ID_Pessoa FK
        date Data_Cadastro
    }
    Funcionario {
        int ID_Funcionario PK
        int ID_Pessoa FK
        string Cargo
    }
    Veterinario {
        int ID_Veterinario PK
        int ID_Funcionario FK
        string CRMV UK
    }
    Especialidade {
        int ID_Especialidade PK
        string Nome
    }
    Veterinario_especialidade {
        int ID_Veterinario FK
        int ID_Especialidade FK
    }
    Animal {
        int ID_Animal PK
        int ID_Cliente FK
        string Nome
        string Especie
    }
    Produto {
        int ID_Produto PK
        string Descricao
        float Valor_Venda
    }
    Servico {
        int ID_Servico PK
        string Descricao
        float Valor_Atual
    }
    Atendimento {
        int ID_Atendimento PK
        int ID_Funcionario FK
        int ID_Cliente FK
        int ID_Animal FK
        int ID_Veterinario FK
        datetime Data_Hora
    }
    Atendimento_produto {
        int ID_Atendimento FK
        int ID_Produto FK
        int Quantidade
        float Valor_Venda
    }
    Atendimento_servico {
        int ID_Atendimento FK
        int ID_Servico FK
        int Quantidade
        float Valor_Venda
    }
    Pagamento {
        int ID_Pagamento PK
        int ID_Atendimento FK
        float Valor_Total
        string Status
    }

    Pessoa ||--o| Cliente : "1:1"
    Pessoa ||--o| Funcionario : "1:1"
    Funcionario ||--o| Veterinario : "1:1"
    
    Veterinario ||--o{ Veterinario_especialidade : "1:N"
    Especialidade ||--o{ Veterinario_especialidade : "1:N"

    Cliente ||--o{ Animal : "1:N"
    
    Cliente ||--o{ Atendimento : "1:N"
    Funcionario ||--o{ Atendimento : "1:N"
    Animal ||--o{ Atendimento : "1:N"
    Veterinario |o--o{ Atendimento : "0..1:N"

    Atendimento ||--o{ Atendimento_produto : "1:N"
    Produto ||--o{ Atendimento_produto : "1:N"
    
    Atendimento ||--o{ Atendimento_servico : "1:N"
    Servico ||--o{ Atendimento_servico : "1:N"

    Atendimento ||--o| Pagamento : "1:1"
```
