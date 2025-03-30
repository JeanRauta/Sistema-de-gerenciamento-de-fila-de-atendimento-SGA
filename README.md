


# Sistema de gerenciamento de fila de atendimento ([Novo SGA](https://novosga.org/docs/))

Este documento é um tutorial de instalação do Sistema de gerenciamento de fila de atendimento [Novo SGA](https://novosga.org/docs/). O objetivo é fornecer orientações claras para instalar e configurar o painel de senhas.

## Observações
- O tutorial foi desenvolvido com base no sistema **Ubuntu server 24.04**, mas pode ser executado em **Ubuntu 24.04**, **Windows WSL**, entre outros.

## 1. Instalando Docker

1. Certifique-se de ter todos os pacotes atualizados executando:
	> **Nota:** a atualização dos pacotes é opcional.
```bash
sudo apt update && sudo apt upgrade -y
```
2. Instale pacotes que permitem o uso de HTTPS para downloads seguros
```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```
3. Faça o download da chave GPG do repositório oficial do Docker usando o `curl`
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
4. Adicione o repositório oficial do Docker ao sistema Ubuntu
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
5. Atualize os repositórios
```bash
 sudo apt update
```
6. Instale o Docker
```bash
 sudo apt install docker-ce
```
7. Verifique se o Docker foi instalado com sucesso
```bash
 docker --version
```
8. Adicione o seu usuário ao grupo docker
```bash
 sudo usermod -aG docker ${USER}
 su - ${USER}
```

## 2. Instalando Docker Compose

1. Crie o diretório para plugins
```bash
 mkdir -p ~/.docker/cli-plugins/
```
2. Baixe o Docker Compose
```bash
 curl -SL https://github.com/docker/compose/releases/download/v2.27.1/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose
```
3. Dê permissão de execução ao Docker Compose
```bash
 chmod +x ~/.docker/cli-plugins/docker-compose
```
4. Verifique se o Docker Compose foi instalado com sucesso
```bash
 docker compose --version
```

## 3. Instalando o Portainer

Crie um volume para armazenar os dados do Portainer com o comando:

```bash
sudo docker volume create portainer_data
```
## 4. Executando o Portainer

Execute o Portainer com o seguinte comando:

```bash
sudo docker run -d -p 8000:8000 -p SUA_PORTA_LOCAL:SUA_PORTA_CONTAINER --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:lts
```

- **SUA_PORTA_LOCAL**: Substitua pela porta local que você deseja expor no seu computador ou servidor.

- **SUA_PORTA_CONTAINER**: Substitua pela porta do container.
> **Nota:** Use a porta `9443` apenas se houver um certificado SSL configurado.

## 5. Acessando o Portainer

Para acessar o Portainer, abra o navegador e digite o seguinte endereço:

```
http://SEU_IP:PORTA
```

- **SEU_IP**: Substitua pelo endereço IP do seu computador ou servidor.
- **PORTA**: Substitua pela porta que foi configurada para o Portainer.

Ao acessar, crie um usuário e senha para gerenciar o ambiente do Portainer.

## 6. Configurando o IP do Ambiente

Após acessar o Portainer, siga os passos abaixo para ajustar o IP do ambiente:

1. No menu, clique no **ícone de lápis** ao lado do ambiente que deseja editar.
2. Altere o campo **Public IP** para o IP do servidor.

## 7. Criando o Ambiente do Novo SGA

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
