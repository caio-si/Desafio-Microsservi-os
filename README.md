# Desafio-Microsservi-os
Desafio Microsserviços

Implementação da Estrutura de Microsserviços com Docker
1. Planejamento da Arquitetura
Comecei o projeto pensando na arquitetura dos microsserviços que quero criar. Decidi que minha aplicação terá dois serviços principais:

Serviço de Autenticação: responsável por gerenciar o login e registro de usuários.
Serviço de Produtos: encarregado de gerenciar informações sobre os produtos disponíveis.
2. Criando o Repositório no GitHub
Criei um novo repositório no GitHub chamado my-microservices. Para organizar melhor, fiz um fork do repositório original mencionado no desafio. Agora, tenho uma base para trabalhar e manter referências diretas ao código original.

3. Estruturando o Projeto
No repositório, criei a seguinte estrutura de diretórios:

bash
Copiar código
/my-microservices
    /auth-service
        /Dockerfile
        /app
    /product-service
        /Dockerfile
        /app
    docker-compose.yml
Essa estrutura me ajudará a manter tudo organizado e fácil de entender.

4. Desenvolvendo os Microsserviços
Para o serviço de autenticação, criei um Dockerfile com o seguinte conteúdo:

Dockerfile
Copiar código
# Use uma imagem base do Node.js
FROM node:14

# Define o diretório de trabalho
WORKDIR /app

# Copia os arquivos de dependências
COPY package*.json ./

# Instala as dependências
RUN npm install

# Copia o restante dos arquivos do serviço
COPY . .

# Expõe a porta em que a aplicação irá rodar
EXPOSE 3000

# Comando para iniciar o serviço
CMD ["npm", "start"]
Fiz algo semelhante para o serviço de produtos, garantindo que ambos os serviços possam ser construídos e executados.

5. Criando o docker-compose.yml
Em seguida, criei o arquivo docker-compose.yml na raiz do projeto para orquestrar os serviços. O conteúdo ficou assim:

yaml
Copiar código
version: '3'

services:
  auth-service:
    build:
      context: ./auth-service
    ports:
      - "3001:3000"

  product-service:
    build:
      context: ./product-service
    ports:
      - "3002:3000"
Isso garante que o serviço de autenticação será acessível em http://localhost:3001 e o serviço de produtos em http://localhost:3002.

6. Testando Localmente
Com tudo configurado, abri o terminal no diretório raiz do projeto e executei:

bash
Copiar código
docker-compose up --build
