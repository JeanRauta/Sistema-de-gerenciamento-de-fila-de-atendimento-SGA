

# Sistema de gerenciamento de fila de atendimento ([Novo SGA](https://novosga.org/docs/))

Este documento é um tutorial de instalação do Sistema de gerenciamento de fila de atendimento [Novo SGA](https://novosga.org/docs/). O objetivo é fornecer orientações claras para instalar e configurar o painel de senhas.

## Observações
- O tutorial foi desenvolvido com base no sistema **Ubuntu server 24.04**, mas pode ser executado em **Ubuntu 24.04**, **Windows WSL**, entre outros.

## 1. Instalando Docker e Docker Compose

Siga as instruções da documentação oficial para instalar o [Docker](https://docs.docker.com/get-docker/) e o [Docker Compose](https://docs.docker.com/compose/install/).

## 2. Instalando o Portainer

Crie um volume para armazenar os dados do Portainer com o comando:

```bash
sudo docker volume create portainer_data
```
## 3. Executando o Portainer

Execute o Portainer com o seguinte comando:

```bash
sudo docker run -d -p 8000:8000 -p SUA_PORTA_LOCAL:SUA_PORTA_CONTAINER --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:lts
```

- **SUA_PORTA_LOCAL**: Substitua pela porta local que você deseja expor no seu computador ou servidor.

- **SUA_PORTA_CONTAINER**: Substitua pela porta do container.
> **Nota:** Use a porta `9443` apenas se houver um certificado SSL configurado.

## 4. Acessando o Portainer

Para acessar o Portainer, abra o navegador e digite o seguinte endereço:

```
http://SEU_IP:PORTA
```

- **SEU_IP**: Substitua pelo endereço IP do seu computador ou servidor.
- **PORTA**: Substitua pela porta que foi configurada para o Portainer.

Ao acessar, crie um usuário e senha para gerenciar o ambiente do Portainer.

## 5. Configurando o IP do Ambiente

Após acessar o Portainer, siga os passos abaixo para ajustar o IP do ambiente:

1. No menu, clique no **ícone de lápis** ao lado do ambiente que deseja editar.
2. Altere o campo **Public IP** para o IP do servidor.

## 6. Criando o Ambiente do Novo SGA

Siga as instruções para criar o ambiente no Portainer:

1. Acesse o site oficial do Novo SGA e copie o código do Docker Compose disponível em: [Novo SGA - Instalação via Docker](https://novosga.org/docs/#/2.1/install-docker)

2. No Portainer, na barra lateral, clique em **Stacks**.

3. Clique em **Add Stack**.

4. No editor de texto da interface, cole o código do Docker Compose copiado.

5. No código, edite a variável de ambiente `MERCURE_CONSUMER_URL`, substituindo o IP da URL pelo IP do seu servidor.

6. Clique em **Deploy the Stack** para iniciar a criação dos containers.

7. Após a criação dos containers, vá até a seção **Containers** para ver as portas onde cada serviço está rodando.

---

Após a conclusão dessas etapas, o sistema estará pronto para uso.

### Informações Importantes:
- O usuário inicial configurado nos containers é **admin**.
- A senha padrão para o usuário **admin** é **123456**.

> **Dica de segurança:** Recomenda-se alterar a senha do usuário administrador após o primeiro login para garantir a segurança do sistema.
