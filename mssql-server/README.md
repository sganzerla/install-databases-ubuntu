# mssql-server

## Pré requisitos

| ITEM                   | CONDIÇÃO |
| ---------------------- | -------- |
| Mémoria RAM            | 2GB      |
| Espaço em disco        | 6GB      |
| Velocidade processador | 2GHz     |
| Núcleos processador    | 2        |
| Tipo processador       | x64      |

## Licenciamento by [Microsoft](https://www.microsoft.com/pt-br/sql-server/sql-server-2017-pricing)

| Edições do SQL Server 2017 | Ideal para…                                                                                                                                                                                        | Modelo de licenciamento | Disponibilidade do canal                            | Preço Open No Level (US$)                              |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------- | --------------------------------------------------- | ------------------------------------------------------ |
| Express                    | Banco de dados de nível básico gratuito ideal para aprendizado, além da criação de aplicativos de área de trabalho e aplicativos controlados por dados de servidores pequenos, de até 10 GB.       | Não aplicável           | Download gratuito                                   | Gratuito                                               |
| Web                        | Plataforma de dados segura, econômica e altamente escalável para sites públicos. Disponível somente para provedores de serviços de terceiros.                                                      | Não aplicável           | Somente hospedagem                                  | Consulte seu parceiro de hospedagem para saber o preço |
| Developer                  | Versão completa do software SQL Server que permite aos desenvolvedores criar, testar e demonstrar de maneira econômica os aplicativos baseados no SQL Server.                                      | Por usuário             | Download gratuito                                   | Gratuito                                               |
| Standard - servidor + CAL  | Funcionalidades básicas de gerenciamento de dados e business intelligence para workloads não críticos com recursos mínimos de TI.                                                                  | Servidor + CAL          | Licenciamento por volume, hospedagem, FPP de varejo | $931                                                   |
| Standard - por núcleo      | Funcionalidades básicas de gerenciamento de dados e business intelligence para workloads não críticos com recursos mínimos de TI.                                                                  | Por núcleo              | Licenciamento por volume, hospedagem                | $3,717                                                 |
| Enterprise                 | Performance abrangente de missão crítica para requisitos exigentes de banco de dados e business intelligence. Oferece os mais elevados níveis de serviço e performance para workloads da Camada 1. | Por núcleo              | Licenciamento por volume, hospedagem                | $14,256                                                |

Observações:

    [1]Os clientes que precisam de um data warehouse de processamento massivo paralelo agora têm acesso a um data warehouse paralelo por meio das licenças de núcleos Enterprise Edition com Software Assurance. O data warehouse paralelo faz parte do Microsoft Analytics Platform System.

    [2]As edições vendidas no modelo de licenciamento por núcleo são vendidas como pacotes de 2 núcleos.

    [3]Os preços representam o preço de varejo estimado Open No Level (NL). Para obter preços específicos, entre em contato com seu revendedor da Microsoft.

    [4]As CALs (licenças de acesso para cliente) são obrigatórias para todos os usuários ou dispositivos que acessam um servidor no modelo de licenciamento Servidor + CAL. Consulte os direitos de uso do produto para obter detalhes.

## Instalação MSQL Server

### Observação

A instalação deste tutorial aponta para o repositório do `Ubuntu 18.04` enquanto o `20.04` não está disponível.

Antes de iniciar a instalação realizar os seguintes comandos a fim de atualizar o sistema operacional:

    ```
    sudo apt-get update
    sudo apt-get upgrade -y
    ```

### Add Chave [GPG](https://pt.wikipedia.org/wiki/GNU_Privacy_Guard)

Importar chaves `GPG` do repositório público:

    ```
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

### Registro no SourceList

Registrar repositório do `MSQL Server` no `SourceList`

    ```
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2019.list)"
    ```

### Instalando MSQL Server

Realizando a instalação

    ```
    sudo apt-get update
    sudo apt-get install -y mssql-server
    ```

Configurando instância, escolha da versão, idioma e definição de senha alfanumérica.

Especifique uma senha forte para a conta SA (comprimento mínimo de 8 caracteres, incluindo letras maiúsculas e minúsculas, 10 dígitos básicos e/ou símbolos não alfanuméricos.

    ```
    sudo /opt/mssql/bin/mssql-conf setup
    ```

Verificar se o serviço está rodando

    ```
    systemctl status mssql-server --no-pager
    ```

### Porta Firewall

Para dar acesso externo necessário abrir porta `TCP` do `SQL Server` no `firewall` o padrão é 1433.

    ```
    sudo apt-get install ufw
    sudo ufw allow 1433/tcp
    sudo ufw enable
    sudo ufw status verbose
    ```

### Alterando porta padrão

Substituir porta padrão 1433

    ```
    sudo /opt/mssql/bin/mssql-conf set network.tcpport <new_tcp_port>
    ```

Reiniciar o serviço

    ```
    sudo systemctl restart mssql-server
    ```

Conectando ao banco

    ```
    sqlcmd -S localhost,<new_tcp_port> -U test -P test
    ```

## Instalação Ferramentas Gerenciamento

Para criar um banco de dados, é necessário conectar-se a uma ferramenta que pode executar instruções `Transact-SQL` no `SQL Server`. As seguintes etapas instalam as ferramentas de linha de comando do `SQL Server`: [sqlcmd](https://docs.microsoft.com/pt-br/sql/tools/sqlcmd-utility?view=sql-server-ver15) e [bcp](https://docs.microsoft.com/pt-br/sql/tools/bcp-utility?view=sql-server-ver15).

### mssql-tools

Importar as chaves `GPG` do repositório público.

    ```
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

Registro no SourceList

    ```
    curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
    ```

Instalar msql-tools

    ```
    sudo apt-get update
    sudo apt-get install mssql-tools unixodbc-dev
    ```

### Opcional comando sqlcmd/bcp

Tornar comando `sqlcmd/bcp` disponível no shell de Bash para sessões de logon

    ```
    echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
    ```

Tornar comando `sqlcmd/bcp` disponível no shell de Bash para sessões interativas que não são de logon

    ```
    echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
    source ~/.bashrc
    ```

## Testando Conexão localhost

Utilizando o `sqlcmd` para conectar-se a uma instância local do `MSQL Server`.

### Conectando

Execute o sqlcmd com parâmetros para o nome do SQL Server (-S), o nome de usuário (-U) e a senha (-P). Neste tutorial, você está se conectando localmente, portanto, o nome do servidor é localhost. O nome de usuário é SA e a senha é a mesma fornecida para a conta SA durante a instalação.

    ```
    sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

Pode ser omitido o comando da senha ela será exigida na linha de comando

    ```
    sqlcmd -S localhost -U SA
    ```

A conexão estará correta quando o shel estiver com o texto `1>`.

### Criando banco de dados

Criando base dados

    ```
    CREATE DATABASE TestDB
    GO
    ```

Inserindo dados

    ```
    USE TestDB
    CREATE TABLE Inventory (id INT, name NVARCHAR(50), quantity INT)
    INSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);
    GO
    ```

Selecionar dados

    ```
    SELECT * FROM Inventory WHERE quantity > 152;
    GO
    ```

Sair prompt

    ```
    QUIT
    ```

### Deletando base de dados

    ```
    USE MASTER;
    ALTER DATABASE [my_database] SET SINGLE_USER WITH ROLLBACK IMMEDIATE;
    DROP DATABASE [my_database];
    
    ```


## Fonte

[Microsoft](https://docs.microsoft.com/pt-br/sql/linux/quickstart-install-connect-ubuntu?view=sql-server-ver15) Acessado em Maio 2020.
