# TRILHA BÁSICA, ATIVIDADE DE BANCO DE DADOS

---

# :pushpin: Índece

- [Projeto](#-Projeto)
- [Instalação](#construction_worker-instalação)
- [Características](#-Características)
- [Autor](#-Autor)
- [Testado no Sistema Operacional](#-Testado-no-Sistema-Operacional)

---

## 💻 Projeto

ATIVIDADE TRILHA BÁSICA - SQL BÁSICO 🚀

---

# :construction_worker: Instalação

**Você precisa instalar o [Mysql 8](https://dev.mysql.com/downloads/installer/),  embaixo segue as resposta da atividade banco de dados :**

```
TAREFA DE BANCO D DADOS

-- CRIAR BANCO DE DADOS

CREATE DATABASE restauranre;

USE restauranre;

-- CRIAR TABELAS

DROP TABLE IF EXISTS cozinha;

CREATE TABLE cozinha (
  id INT(10) NOT NULL AUTO_INCREMENT,
  horaAbertura INT(11) DEFAULT NULL,
  horaFechamento INT(11) DEFAULT NULL,
  pratoPrincipal VARCHAR(30) ,
  numeroDePratos INT(10) DEFAULT NULL,
  tempoDoPreparo INT(10) DEFAULT NULL,
  numeroDeCozinheiros INT(10) DEFAULT NULL,
  tipo VARCHAR(80) ,
  id_funcionario INT(10) DEFAULT NULL,
  id_ingrediente INT(10) DEFAULT NULL,
  PRIMARY KEY  (id),
  KEY id (id),
  KEY id_2 (id),
  KEY id_funcionario (id_funcionario),
  KEY id_ingrediente  (id_ingrediente ), 
  CONSTRAINT cozinha_ibfk_1 FOREIGN KEY (id_funcionario) REFERENCES funcionario (id),
  CONSTRAINT cozinha_ibfk_2  FOREIGN KEY (id_ingrediente ) REFERENCES ingrediente  (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

DROP TABLE IF EXISTS funcionario;

CREATE TABLE funcionario (
  id INT(10) NOT NULL AUTO_INCREMENT,
  nome VARCHAR(60) ,
  atividade VARCHAR(60),
  PRIMARY KEY  (id)
) ENGINE=INNODB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;



DROP TABLE IF EXISTS ingrediente;

CREATE TABLE ingrediente (
  id INT(10) NOT NULL AUTO_INCREMENT,
  nomeDosIngrediente VARCHAR(60) ,
  dataValidade VARCHAR(60),
  PRIMARY KEY  (id)
) ENGINE=INNODB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

-- Incluir 10 itens na tabela de funcionários

INSERT INTO funcionario (nome, atividade)
VALUES ('DANIEL', 'COZINHEIRO 3');

INSERT INTO funcionario (nome, atividade)
VALUES ('PEDRO', 'AUX. DE COZINHA');

INSERT INTO funcionario (nome, atividade)
VALUES ('SAULO', 'CHEFE DE COZINHA');

INSERT INTO funcionario (nome, atividade)
VALUES ('AMANDA', 'SALADEIRA');

INSERT INTO funcionario (nome, atividade)
VALUES ('PAULO', 'AJUDANTE');

INSERT INTO funcionario (nome, atividade)
VALUES ('FLÁVIA', 'COZINHEIRA');

INSERT INTO funcionario (nome, atividade)
VALUES ('GUSTAVO', 'COZINHEIRO 1');

INSERT INTO funcionario (nome, atividade)
VALUES ('LUÍS', 'AJUDANTE');

INSERT INTO funcionario (nome, atividade)
VALUES ('MARCOS', 'COZINHEIRO 2');

INSERT INTO funcionario (nome, atividade)
VALUES ('JOÃO', 'AJUDANTE');


-- Incluir 5 itens na tabela de cozinha

INSERT INTO cozinha (horaAbertura, horaFechamento, pratoPrincipal, numeroDePratos, tempoDoPreparo, numeroDeCozinheiros, tipo, id_funcionario, id_ingrediente)
VALUES (8, 23, 'Yakissoba', 10, 30, 32, 'Cozinha Chinesa', 1, 1);

INSERT INTO cozinha (horaAbertura, horaFechamento, pratoPrincipal, numeroDePratos, tempoDoPreparo, numeroDeCozinheiros, tipo, id_funcionario, id_ingrediente)
VALUES (11, 22, 'Peedan', 10, 30, 32, 'Cozinha Chinesa', 2, 2);

INSERT INTO cozinha (horaAbertura, horaFechamento, pratoPrincipal, numeroDePratos, tempoDoPreparo, numeroDeCozinheiros, tipo, id_funcionario, id_ingrediente)
VALUES (9, 23, 'feijoada', 22, 50, 22, 'Cozinha Mineira', 3, 3);

INSERT INTO cozinha (horaAbertura, horaFechamento, pratoPrincipal, numeroDePratos, tempoDoPreparo, numeroDeCozinheiros, tipo, id_funcionario, id_ingrediente)
VALUES (8, 20, 'Espaguete', 12, 41, 14, 'Cozinha Italiana', 4, 4);

INSERT INTO cozinha (horaAbertura, horaFechamento, pratoPrincipal, numeroDePratos, tempoDoPreparo, numeroDeCozinheiros, tipo, id_funcionario, id_ingrediente)
VALUES (9, 19, 'Tutu de Feijão', 15, 42, 13, 'Cozinha Mineira', 5, 5);

-- Incluir 8 na tabela e ingredientes

INSERT INTO ingrediente (nomeDosIngrediente, dataValidade)
VALUES ('Macarrão', '01/04/2021');

INSERT INTO ingrediente (nomeDosIngrediente, dataValidade)
VALUES ('Carne', '31/03/2021');

INSERT INTO ingrediente (nomeDosIngrediente, dataValidade)
VALUES ('Champignon', '21/04/2021');

INSERT INTO ingrediente (nomeDosIngrediente, dataValidade)
VALUES ('Brócolis', '11/03/2021');

INSERT INTO ingrediente (nomeDosIngrediente, dataValidade)
VALUES ('Molho', '19/02/2021');

INSERT INTO ingrediente (nomeDosIngrediente, dataValidade)
VALUES ('Farinha', '22/03/2021');

INSERT INTO ingrediente (nomeDosIngrediente, dataValidade)
VALUES ('Linguiça', '23/04/2021');

INSERT INTO ingrediente (nomeDosIngrediente, dataValidade)
VALUES ('Carne de Porco', '01/05/2021');

-- Criar uma consulta que retorne a quantidade de cozinhas cadastradas NO banco de dados.

SELECT COUNT(id) AS qtd, cz.tipo AS cozinhas  FROM cozinha AS cz
	GROUP BY cz.tipo 

-- Criar uma consulta que possua um filtro, buscando AS cozinhas que possuam o horário de fechamento AS 22 horas.

SELECT * FROM cozinha WHERE horaFechamento = 22;

-- Criar uma consulta que liste quais ingredientes estão vencidos.
SELECT 
        ing.nomeDosIngrediente AS ingredientes, ing.dataValidade AS vencido
    FROM ingrediente AS ing	
     WHERE ing.dataValidade < CURDATE();
	
  -- Criar uma consulta que realize a junção das tabelas Cozinha, Ingrediente e Funcionario e informe AS cozinhas não possuam ingredientes.

SELECT 
        cz.tipo as cozinha, ing.nomeDosIngrediente as semIngrediente
    FROM cozinha as cz

	  INNER JOIN ingrediente as ing
	  ON cz.id_ingrediente = ing.id 
	
	  INNER JOIN funcionario AS fun
	  ON cz.id_funcionario = fun.id 
	  
	  WHERE  ing.nomeDosIngrediente  = '';


-- Criar uma consulta que realize a junção das tabelas Cozinha, Ingrediente e Funcionario e informe AS cozinhas que possuam número de funcionários maior que 4;

SELECT 
        cz.tipo as cozinha, cz.numeroDeCozinheiros as numeroDeFuncionario
    FROM cozinha as cz

	  INNER JOIN ingrediente as ing
	  ON cz.id_ingrediente = ing.id 
	
	  INNER JOIN funcionario AS fun
	  ON cz.id_funcionario = fun.id 
	  
	  WHERE cz.numeroDeCozinheiros  > 4;

```

---

## 📋 Características

### Documentação

- [x] Criar Banco de Dados chamado Restaurante
- [x] Criar AS tabelas Cozinha, Ingrediente e Funcionario
- [x] Incluir 5 itens na tabela de cozinha, 8 na tabela e ingredientes e 10 na tabela de funcionários.
- [x] Criar uma consulta que retorne a quantidade de cozinhas cadastradas no banco de dados.
- [x] Criar uma consulta que possua um filtro, buscando as cozinhas que possuam o horário de fechamento as 22 horas.
- [x] Criar uma consulta que liste quais ingredientes estão vencidos.
- [x] Criar relacionamentos entre AS tabelas:
      Uma cozinha pode ter mais de um ingrediente.
      Uma cozinha também pode ter mais de um funcionário.
      Alterar o banco para possibilitar estes relacionamentos.
- [x] Criar uma consulta que realize a junção das tabelas Cozinha, Ingrediente e Funcionario e informe AS cozinhas não possuam ingredientes.
- [x] Criar uma consulta que realize a junção das tabelas Cozinha, Ingrediente e Funcionario e informe as cozinhas que possuam número de funcionários maior que 4;

---

## 👤 Autor

**Daniel Silva**

Entre em contato comigo em um dos seguintes lugares!

- Twitter: [@DanielSilva](https://twitter.com/danielsilvatsi)
- Github: [@DanielSilva](https://github.com/SilvaTs)
- Linkedin: [@DanielSilva](https://www.linkedin.com/in/daniel-silva-tsi/)

---

## 🧪 Testado no Sistema Operacional

- Windows (por @danielsilva)
