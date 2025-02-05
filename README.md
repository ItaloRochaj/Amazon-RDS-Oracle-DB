# Criando e Gerenciando um Banco de Dados na AWS com Amazon RDS

Aprenda a configurar e interagir com uma instância de banco de dados gerenciada pela AWS, conectando-a a um aplicativo web para armazenamento e manipulação de dados.

## Introdução

O **Amazon Relational Database Service (Amazon RDS)** simplifica a criação, operação e escalabilidade de bancos de dados relacionais na nuvem. Ele gerencia tarefas administrativas complexas, permitindo que você foque no desenvolvimento do seu aplicativo.

O Amazon RDS suporta seis mecanismos de banco de dados: **Amazon Aurora, Oracle, Microsoft SQL Server, PostgreSQL, MySQL e MariaDB**.

## O que você aprenderá?

Ao concluir este laboratório, você será capaz de:

- Criar uma instância de banco de dados Amazon RDS altamente disponível.
- Configurar permissões para conexões seguras entre a instância e um servidor web.
- Interagir com o banco de dados por meio de um aplicativo web.


## Estrutura do Laboratório

Você iniciará com a seguinte infraestrutura:

![Arquitetura inicial](https://github.com/ItaloRochaj/Amazon-RDS-Oracle-DB/blob/main/projects%20images/Infraestrutura%20Inicial.png)

Após a configuração, sua infraestrutura estará assim:

![Arquitetura final](https://github.com/ItaloRochaj/Amazon-RDS-Oracle-DB/blob/main/projects%20images/Infraestrutura%20Final.png)


## Acessando o AWS Management Console

1. No canto superior direito destas instruções, clique em **Iniciar laboratório**.
2. Aguarde o status mudar para **pronto** (círculo verde no canto superior esquerdo).
3. Clique no **círculo verde** para abrir o **AWS Management Console**.
4. Caso uma nova aba não seja aberta, ative pop-ups no seu navegador.
5. Mantenha o console aberto para acompanhar os passos a seguir.

## Passo 1: Criando um Grupo de Segurança para o Banco de Dados

1. Acesse **Serviços > VPC** no AWS Management Console.
2. No menu lateral, clique em **Grupos de Segurança**.
3. Clique em **Criar grupo de segurança** e preencha:
   - **Nome:** DB Security Group
   - **Descrição:** Permite acesso do Web Security Group
   - **VPC:** Escolha a VPC do laboratório
4. Adicione uma regra de entrada:
   - **Tipo:** MySQL/Aurora (3306)
   - **Fonte:** Web Security Group
5. Clique em **Criar grupo de segurança**.

## Passo 2: Criando um Grupo de Sub-rede para o Banco de Dados

1. Acesse **Serviços > RDS** no AWS Management Console.
2. No menu esquerdo, clique em **Grupos de sub-rede**.
3. Clique em **Criar grupo de sub-rede de banco de dados** e preencha:
   - **Nome:** DB Subnet Group
   - **Descrição:** Grupo de sub-rede para o banco de dados
   - **VPC:** Escolha a VPC do laboratório
4. Adicione sub-redes para pelo menos duas **Zonas de Disponibilidade**:
   - **Zona 1:** 10.0.1.0/24
   - **Zona 2:** 10.0.3.0/24
5. Clique em **Criar**.

## Passo 3: Criando a Instância Amazon RDS

1. No menu esquerdo do RDS, clique em **Bancos de Dados**.
2. Selecione **Criar banco de dados** e escolha **Criação padrão**.
3. Configure os seguintes parâmetros:
   - **Mecanismo:** MySQL
   - **Modelo:** Dev/Teste
   - **Disponibilidade:** Multi-AZ
   - **Identificador:** lab-db
   - **Usuário mestre:** main
   - **Senha:** lab-password
   - **Classe da instância:** db.t3.medium
   - **Armazenamento:** SSD
   - **VPC:** Escolha a VPC do laboratório
   - **Grupo de segurança:** DB Security Group
4. Em **Configuração adicional**, defina:
   - **Nome do banco de dados inicial:** lab
   - **Desative backups automáticos** (para fins de laboratório).
5. Clique em **Criar banco de dados**.
6. Aguarde a instância ficar disponível.
7. Copie o **Endpoint** gerado para uso posterior.

## Passo 4: Conectando ao Banco de Dados via Aplicativo Web

1. No laboratório, copie o **endereço IP** do **WebServer**.
2. No navegador, cole o IP e pressione **Enter**.
3. No aplicativo, clique na opção **RDS**.
4. Preencha os campos de conexão com:
   - **Ponto final:** Cole o endpoint do banco de dados.
   - **Banco de dados:** lab
   - **Usuário:** main
   - **Senha:** lab-password
5. Clique em **Enviar**.
6. O aplicativo exibirá um **Address Book**, permitindo adicionar, editar e excluir contatos armazenados no RDS.
   ![Interface Web](https://github.com/ItaloRochaj/Amazon-RDS-Oracle-DB/blob/main/projects%20images/Interface%20Web%20App.png)

## Conclusão
    
Recursos adicionais
Para obter mais informações sobre o treinamento e a certificação da AWS, consulte https://aws.amazon.com/training/ . 
 🚀

