Docker For My Studies

# 🐳 Guia Rápido: Comandos Docker Essenciais

Uma lista dos comandos Docker mais utilizados no dia a dia, organizados por categoria.

## 🚀 Gerenciamento de Contêineres (O Dia a Dia)

Comandos para criar, listar e interagir com seus contêineres.

* **`docker run [OPÇÕES] [IMAGEM]`**: O comando principal. Cria e inicia um novo contêiner a partir de uma imagem.
    * **Flags comuns:**
        * `docker run -d nginx` (Modo "detached", roda em segundo plano)
        * `docker run -p 8080:80 nginx` (Mapeia a porta 8080 do host para a 80 do contêiner)
        * `docker run --name web_server nginx` (Dá um nome específico ao contêiner)
        * `docker run -it ubuntu /bin/bash` (Inicia e acessa o terminal do contêiner)

* **`docker ps`**: Lista todos os contêineres que estão **em execução**.

* **`docker ps -a`**: Lista **TODOS** os contêineres (em execução e parados).

* **`docker stop [NOME_OU_ID]`**: Para um contêiner em execução de forma "graciosa".

* **`docker start [NOME_OU_ID]`**: Inicia um contêiner que estava parado.

* **`docker restart [NOME_OU_ID]`**: Reinicia um contêiner.

* **`docker rm [NOME_OU_ID]`**: Remove um contêiner (ele deve estar parado primeiro).
    * `docker rm -f [NOME_OU_ID]` (Força a remoção, mesmo se estiver rodando).

---

## 📦 Gerenciamento de Imagens

Comandos para gerenciar as "plantas" dos seus contêineres.

* **`docker images`**: Lista todas as imagens baixadas localmente.

* **`docker pull [NOME_DA_IMAGEM]`**: Baixa uma imagem do Docker Hub (ou outro registry).
    * Ex: `docker pull ubuntu:22.04`

* **`docker rmi [NOME_OU_ID_DA_IMAGEM]`**: Remove uma imagem local.
    * *Nota: Você não pode remover uma imagem se ela estiver sendo usada por um contêiner.*

* **`docker tag [IMAGEM_ATUAL] [NOVO_NOME]`**: "Renomeia" uma imagem (cria um novo apelido/tag).

---

## 🕵️ Inspeção e Debug (Diagnóstico)

Quando você precisa saber o que está acontecendo dentro de um contêiner.

* **`docker logs [NOME_OU_ID]`**: Mostra a saída (logs) de um contêiner.
    * `docker logs -f [NOME_OU_ID]` (Mostra os logs "ao vivo", como um `tail -f`).

* **`docker exec -it [NOME_OU_ID] [COMANDO]`**: Executa um comando dentro de um contêiner que já está rodando.
    * **O mais usado:** `docker exec -it meu_container /bin/bash` (ou `sh`) para "entrar" no terminal do contêiner.

* **`docker inspect [NOME_OU_ID]`**: Mostra todos os detalhes de baixo nível (IP, volumes, etc.) de um contêiner ou imagem em formato JSON.

---

## 🏗️ Build e Registries (Construção e Compartilhamento)

Para criar suas próprias imagens e compartilhá-las.

* **`docker build -t [MEU_APP]:[TAG] .`**: Constrói uma nova imagem a partir de um `Dockerfile`.
    * `-t` é para "taggear" (ex: `meu_app:v1`).
    * O `.` no final indica que o `Dockerfile` está no diretório atual.

* **`docker login`**: Faz o login em um registry (como o Docker Hub).

* **`docker push [NOME_DA_IMAGEM]`**: Envia sua imagem local para um registry.

---

## 🧹 Limpeza do Sistema

O Docker pode ocupar muito espaço em disco. Estes comandos ajudam a limpar.

* **`docker system prune`**: Remove contêineres parados, redes não utilizadas, imagens "pendentes" (dangling) e cache de build.

* **`docker system prune -a`**: Versão mais agressiva que remove **todas** as imagens que não estão sendo usadas por pelo menos um contêiner.

* **`docker volume prune`**: Remove volumes que não estão sendo usados por nenhum contêiner.

---

## ✨ Menção Honrosa: Docker Compose

Embora seja um comando separado (`docker compose`), é a ferramenta mais comum para gerenciar aplicações com **múltiplos contêineres** (ex: um app web + um banco de dados).

* **`docker compose up`**: Inicia todos os serviços definidos em um arquivo `docker-compose.yml`.
* **`docker compose down`**: Para e remove todos os contêineres, redes e volumes criados pelo `up`.

