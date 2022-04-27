# AWS Simple Exemple

Um projeto simples, feito como avaliação do 7° periodo de Engenharia de Software na Universidade Uniamerica / Descomplica

## Setup na AWS

### Banco de dados

Subir uma instancia RDS Free Tier usando Postgres

**Configurações**:

- Banco: PostgreSQL (Versão usada durante testes: PostgreSQL 13.4-R1)
- Verificar se disponibilidade é "Instancia de banco de dados unica"
- Modelos: Nivel Gratuito
- Credenciais: ***
- Criar um grupo de segurança VPC
- Adicionar um nome para o banco de dados inicial

### Backend

É necessario configurar o Git Hub Actions para realizar o build do Backend e o deploy da imagem no Docker Hub

**Configurações**

- Secrets do Docker Hub

Após buildado, verifique se foi criado e/ou atualizado a imagem no perfil do Docker Hub

Em seguida, subir uma instancia EC2 Free Tier na AWS

**Configurações**

- Imagem: Ubuntu (Versão usada durante testes: Ubuntu Server 20.04 LTS)
- Garantir que esteja na mesma subnet privada do banco de dados
- Realizar a instalação do Docker na máquina
- Logar com o Docker dentro da instancia

Quando a instancia estiver online e configurada com o docker, é necessario puxar a imagem do Docker Hub e inicia-la com as variaveis de ambiente

```shell
docker run -p 80:5000 -e SERVER_PORT=5000 -e DB_USER=postgres -e DB_PASSWORD=password -e DB_URL=database-1.cky5ttiocteg.us-east-1.rds.amazonaws.com -e DB_PORT=5432 -e DB_NAME=customers saitohbp/aws.simple.example.backend
```

### Frontend

**Configurações**

- Imagem: Ubuntu (Versão usada durante testes: Ubuntu Server 20.04 LTS)
- Garantir que esteja na mesma subnet privada do banco de dados
- Realizar a instalação do Docker na máquina
- Logar com o Docker dentro da instancia

Quando a instancia estiver online e configurada com o docker, é necessario puxar a imagem do Docker Hub e inicia-la com as variaveis de ambiente


```shell
docker run -p 80:80 saitohbp/aws.simple.example.frontend
```