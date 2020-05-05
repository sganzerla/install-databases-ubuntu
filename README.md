# install-msql-ubuntu

Este tutorial mostra como instalar o MSQL Server em um sistema operacional Ubuntu 20.04 e versões mais antigas (testado apenas com 20.04).

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

## Fonte

[Microsoft](https://docs.microsoft.com/pt-br/sql/linux/quickstart-install-connect-ubuntu?view=sql-server-ver15) Acessado em Maio 2020.
