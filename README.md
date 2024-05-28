# MiniFramework MVC

Este é um projeto de um mini framework PHP desenvolvido para fins educacionais. Ele ilustra conceitos básicos de MVC (Model-View-Controller), rotas e integração com o banco de dados utilizando PDO.

## Configuração

### Requisitos

- PHP 7.4 ou superior
- Composer
- MySQL

### Passos para Configuração

1. Clone o repositório:

    ```sh
    git clone https://github.com/Lucas-D-A-Barcellos/Miniframework.git
    cd Miniframework
    ```

2. Instale as dependências do Composer:

    ```sh
    composer install
    ```

3. Configure o banco de dados:

    Crie um banco de dados MySQL chamado `mvc` e importe o seguinte script SQL:

    ```sql
    CREATE TABLE tb_info (
        id INT AUTO_INCREMENT PRIMARY KEY,
        titulo VARCHAR(255) NOT NULL,
        descricao TEXT NOT NULL
    );

    CREATE TABLE tb_produtos (
        id INT AUTO_INCREMENT PRIMARY KEY,
        descricao VARCHAR(255) NOT NULL,
        preco DECIMAL(10, 2) NOT NULL
    );
    ```

4. Configure a conexão com o banco de dados:

    Edite o arquivo `App/Connection.php` com suas credenciais de banco de dados.

    ```php
    <?php

    namespace App;

    class Connection {

        public static function getDb() {
            try {
                $conn = new \PDO(
                    "mysql:host=localhost;dbname=mvc;charset=utf8",
                    "root",
                    ""
                );

                return $conn;

            } catch (\PDOException $e) {
                // Handle exception
            }
        }
    }

    ?>
    ```

5. Inicie o servidor embutido do PHP:

    ```sh
    php -S localhost:8000 -t public
    ```

6. Acesse o projeto em seu navegador:

    ```
    http://localhost:8000
    ```

## Estrutura MVC

### Controllers

- `IndexController.php`: Controlador principal que gerencia as ações `index` e `sobreNos`.

### Models

- `Produto.php`: Modelo para manipulação dos dados da tabela `tb_produtos`.
- `Info.php`: Modelo para manipulação dos dados da tabela `tb_info`.

### Views

- `index.phtml`: View para exibir a lista de produtos.
- `sobre_nos.phtml`: View para exibir informações sobre a empresa.
- `layout1.phtml`: Layout principal utilizado para renderizar as views.

### Roteamento

As rotas são configuradas no arquivo `Route.php`. O método `initRoutes` define as rotas disponíveis no aplicativo.

```php
<?php

namespace App;

use MF\Init\Bootstrap;

class Route extends Bootstrap {

    protected function initRoutes() {
        
        $routes['home'] = array(
            'route' => '/',
            'controller' => 'indexController',
            'action' => 'index'
        ); 

        $routes['sobre_nos'] = array(
            'route' => '/sobre_nos',
            'controller' => 'indexController',
            'action' => 'sobreNos'
        );

        $this->setRoutes($routes);
    }
}

?>


