-- Criação da tabela 'Filmes'
CREATE TABLE Filmes (
    id_filme INT PRIMARY KEY,
    titulo VARCHAR(255),
    genero VARCHAR(100),
    ano_lancamento INT,
    quantidade_estoque INT
);

-- Inserção de dados na tabela 'Filmes'
INSERT INTO Filmes (id_filme, titulo, genero, ano_lancamento, quantidade_estoque) VALUES
(1, 'Homem de Ferro 2', 'Ação, Aventura, Ficção Científica', 2010, 5),
(2, 'Capitão América: O Primeiro Vingador', 'Ação, Aventura, Ficção Científica', 2011, 3),
(3, 'Os Vingadores', 'Ação, Aventura, Ficção Científica', 2012, 7),
(4, 'Guardiões da Galáxia', 'Ação, Aventura, Comédia', 2014, 2),
(5, 'Homem-Aranha: Sem Volta para Casa', 'Ação, Aventura, Ficção Científica', 2021, 4);

-- Criação da tabela 'Clientes'
CREATE TABLE Clientes (
    id_cliente INT PRIMARY KEY,
    nome VARCHAR(255),
    telefone VARCHAR(20),
    endereco VARCHAR(255),
    ultima_locacao DATE 
);

-- Inserção de dados na tabela 'Clientes'
INSERT INTO Clientes (id_cliente, nome, telefone, endereco, ultima_locacao) VALUES
(1, 'João Silva', '(67) 99999-8888', 'Rua das Flores, 123, Centro', NULL),
(2, 'Maria Oliveira', '(67) 98888-7777', 'Avenida Principal, 456, Jardim dos Ipês', NULL),
(3, 'Pedro Souza', '(67) 97777-6666', 'Rua Tranquila, 789, Vila Nova', NULL);

-- Criação da tabela 'Alugueis'
CREATE TABLE Alugueis (
    id_aluguel INT PRIMARY KEY,
    id_filme INT,
    id_cliente INT,
    data_aluguel DATE,
    data_devolucao DATE,
    FOREIGN KEY (id_filme) REFERENCES Filmes(id_filme),
    FOREIGN KEY (id_cliente) REFERENCES Clientes(id_cliente)
);

-- Inserção de dados na tabela 'Alugueis'
INSERT INTO alugueis (id_aluguel, id_filme, id_cliente, data_aluguel, data_devolucao) VALUES
(1, 1, 1, '2023-10-20', '2023-10-25'),  -- João Silva alugou Homem de Ferro 2 em 20/10/2023 e devolveu em 25/10/2023
(2, 3, 2, '2023-11-15', NULL),  -- Maria Oliveira alugou Os Vingadores em 15/11/2023 e ainda não devolveu
(3, 5, 3, '2023-11-05', '2023-11-10'),  -- Pedro Souza alugou Homem-Aranha em 05/11/2023 e devolveu em 10/11/2023
(4, 2, 1, '2023-11-18', '2023-11-22'),  -- João Silva alugou Capitão América em 18/11/2023 e devolveu em 22/11/2023
(5, 4, 2, '2023-11-20', NULL);  -- Maria Oliveira alugou Guardiões da Galáxia em 20/11/2023 e ainda não devolveu

UPDATE Clientes
SET telefone = '(67) 99999-1111'  -- Novo número de telefone
WHERE id_cliente = 1;

-- Seleciona todos os dados do cliente com id_cliente = 2
SELECT * FROM Clientes WHERE id_cliente = 2;

ALTER TABLE Alugueis
ADD CONSTRAINT FK_Aluguel_Cliente 
FOREIGN KEY (id_cliente) 
REFERENCES Clientes(id_cliente) 
ON DELETE CASCADE;

SELECT * FROM Clientes WHERE id_cliente = 2;
