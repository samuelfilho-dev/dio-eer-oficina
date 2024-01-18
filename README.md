# Diagramas De EER 
O repositório possui diagrama de Entidade Relacionamento Estendido no contexto de oficina de carro, seguindo os seguintes requisitos:

  - Sistema de controle e gerenciamento de execução de ordens de serviço em uma oficina mecânica
  - Clientes levam veículos à oficina mecânica para serem consertados ou para passarem por revisões periódicas
  - Cada veículo é designado a uma equipe de mecânicos que identifica os serviços a serem executados e preenche uma OS com data de entrega.
  - A partir da OS, calcula-se o valor de cada serviço, consultando-se uma tabela de referência de mão-de-obra
  - O valor de cada peça também irá compor a OS cliente autoriza a execução dos serviços
  - A mesma equipe avalia e executa os serviços
  - Os mecânicos possuem código, nome, endereço e especialidade
  - Cada OS possui: n°, data de emissão, um valor, status e uma data para conclusão dos trabalhos.


## Diagrama da Oficina
```mermaid
classDiagram
    class Cliente {
      - Interger idCliente
      - String Nome
      - String CPF
      - String Email
      - String Telefone
      - Interger idEndereço
    }

    class Mecânico {
      - Interger idMecânico
      - String Código
      - String Nome
      - String Especialidade
      - String Formação
      - TIME Horas Trabalhadas
      - Interger idEndereço
      - Interger idEquipe
    }

    class `Endereço` {
      - Interger idEndereço
      - String Logradouro
      - String Bairro
      - String Cidade
      - String Complemento
      - String UF
    }

    class `Veículo` {
      - Interger idVeículo
      - String Marca
      - String Modelo
      - String Placa
      - Interger Horímetro
      - Interger idCliente
    }

    class `Manutenção` {
      - Interger idVeículo
      - Interger idEquipe
      - TIMESTAMP Data Da Manutenção
      - Interger Quilometragem
      - String Comentários
    }

    class `Equipe do Mecânico` {
      - Interger idEquipe
      - String Código 
      - String Categoria
    }

    class `Ordem de Serviço` {
      - Interger idOS
      - String Número da OS
      - TIMESTAMP Data da Emissão
      - Double Valor Total
      - ENUM Status
      - Boolean isRevisaoPeriodica
      - TIMESTAMP Data de Aprovação
      - TIMESTAMP Data de Entrega
      - Double Valor da Peças
      - Double Valor dos Serviços
      - Interger idEquipe
      - Interger idCliente
    }

    class `Peça` {
      - Interger idPecas
      - String Referência
      - String Nome
      - String Valor Unitario
      - String Disponbilidade
    }

    class `Serviço` {
      - Interger idServiço
      - String Nome
      - String Categoria do Serviço
      - Double Valor Unitario
    }

    class `Tabela de Referência` {
      - Interger idValorReferência
      - String Nome
      - String Categoria
      - Double Valor de Referência
      - Interger idServiço
    }

    class `Ordem De Serviço_has_Peça` {
      - Interger idOS
      - Interger idPecas
      - Interger Quantidade
    }

    class `Ordem De Serviço_has_Serviço` {
      - Interger idOS
      - Interger idServiços
      - Interger Quantidade
    }

    Cliente "1" .. "1" `Endereço`: Morar
    Cliente "1" --* "N" `Veículo`: Possui
    Cliente "1" --* "N" `Ordem de Serviço`: Aprova
    Mecânico "1" .. "1" `Endereço`: Morar
    `Veículo` "1" --* "N" `Manutenção`: Faz Manutenção
    `Equipe do Mecânico` "1" --* "N" `Mecânico`: Tem
    `Equipe do Mecânico` "1" --* "N" `Manutenção`: Faz Manutenção
    `Equipe do Mecânico` "1" --* "N" `Ordem de Serviço`: Cria
    `Ordem de Serviço` "1" --* "N" `Ordem De Serviço_has_Peça`: Tem
    `Ordem de Serviço` "1" --* "N" `Ordem De Serviço_has_Serviço`: Tem
    `Peça` "1" --* "N" `Ordem De Serviço_has_Peça`: Tem
    `Serviço` "1" --* "N" `Ordem De Serviço_has_Serviço`: Tem
    `Serviço` "1" --* "N" `Tabela de Referência`: Possui
   


```

## Contribuir
 - Se você deseja contribuir para o projeto, siga estes passos:

    1. Faça um fork do repositório.
    2. Crie uma branch para suas modificações: `git checkout -b minha-contribuicao`.
    3. Faça as modificações e commit: `git commit -m "Minha contribuição: Descrição"`.
    4. Envie as modificações para o seu fork: `git push origin minha-contribuicao`.
    5. Abra um pull request para revisão.

 - Colocar estrelas ⭐

## Autor

<table>
  <tr>
    <td align="center"><a href="https://github.com/samuelfilho-dev"><img src="https://avatars.githubusercontent.com/u/81279868?s=400&u=89e596d8d5cc674251c908e45fa47a37db0db3a0&v=4" width="100px;" alt=""/><br/><strong>Samuel Filho</strong></a><br/><a href="https://www.linkedin.com/in/samuelfilho-dev/">LinkedIn</a></td>
  </tr>
</table>