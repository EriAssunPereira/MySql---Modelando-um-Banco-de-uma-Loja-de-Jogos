# MySql-Modelando-um-Banco-de-uma-Loja-de-Jogos

Para modelar um banco de dados para uma loja de jogos online usando MySQL, precisamos considerar várias entidades principais e seus relacionamentos. Vou guiá-lo passo a passo na criação do esquema do banco de dados, utilizando uma abordagem modular para os exemplos de código SQL.

### Passo 1: Definição das Entidades

1. **Usuários**
   - Armazena informações sobre os usuários registrados na loja.

   ```sql
   CREATE TABLE usuarios (
       id_usuario INT PRIMARY KEY AUTO_INCREMENT,
       nome VARCHAR(100) NOT NULL,
       email VARCHAR(100) UNIQUE NOT NULL,
       senha VARCHAR(100) NOT NULL,
       data_registro DATE NOT NULL
   );
   ```

2. **Jogos**
   - Informações detalhadas sobre os jogos disponíveis para venda.

   ```sql
   CREATE TABLE jogos (
       id_jogo INT PRIMARY KEY AUTO_INCREMENT,
       titulo VARCHAR(100) NOT NULL,
       descricao TEXT,
       preco DECIMAL(10, 2) NOT NULL,
       data_lancamento DATE
   );
   ```

3. **Pedidos**
   - Registra os pedidos feitos pelos usuários.

   ```sql
   CREATE TABLE pedidos (
       id_pedido INT PRIMARY KEY AUTO_INCREMENT,
       id_usuario INT,
       data_pedido DATETIME NOT NULL,
       total DECIMAL(10, 2) NOT NULL,
       FOREIGN KEY (id_usuario) REFERENCES usuarios(id_usuario)
   );
   ```

4. **Itens do Pedido**
   - Relaciona os jogos comprados em cada pedido.

   ```sql
   CREATE TABLE itens_pedido (
       id_pedido INT,
       id_jogo INT,
       quantidade INT NOT NULL,
       preco_unitario DECIMAL(10, 2) NOT NULL,
       PRIMARY KEY (id_pedido, id_jogo),
       FOREIGN KEY (id_pedido) REFERENCES pedidos(id_pedido),
       FOREIGN KEY (id_jogo) REFERENCES jogos(id_jogo)
   );
   ```

### Passo 2: Relacionamentos entre as Entidades

- A tabela `pedidos` possui uma chave estrangeira `id_usuario` que referencia a tabela `usuarios`.
- A tabela `itens_pedido` possui chaves estrangeiras `id_pedido` e `id_jogo` que referenciam as tabelas `pedidos` e `jogos`, respectivamente.

### Passo 3: Normalização

- Os campos foram projetados para evitar redundância e garantir a consistência dos dados.
- Cada tabela possui uma chave primária única para identificação única de registros.
- Utilizamos chaves estrangeiras para estabelecer relacionamentos entre as tabelas.

### Passo 4: Consultas Exemplos

- Exemplo de consulta para listar todos os jogos:

  ```sql
  SELECT * FROM jogos;
  ```

- Exemplo de consulta para encontrar pedidos de um usuário específico:

  ```sql
  SELECT * FROM pedidos WHERE id_usuario = 1;
  ```

### Considerações Finais

Este esquema básico cobre as principais entidades e relacionamentos para uma loja de jogos online. Dependendo dos requisitos específicos adicionais (como carrinho de compras, avaliações de jogos, etc.), o esquema pode ser expandido. Certifique-se sempre de ajustar o modelo conforme as necessidades exatas de cada projeto.
