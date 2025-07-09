# 🧩 Guess Game – Deploy Dockerizado

Aplicação web de adivinhação de frases composta por:

- ⚛️ **Frontend React + NGINX** (no mesmo container)
- 🐍 **Backend Flask**
- 🐘 **Banco PostgreSQL**
- 🐳 Orquestração via **Docker Compose**

---

## 🏗️ Estrutura dos Serviços

| Serviço   | Imagem/base      | Versão/Origem  | Função                                           |
|-----------|------------------|---------------|--------------------------------------------------|
| 🐘 db        | postgres         | 16            | Banco de dados relacional (PostgreSQL)           |
| 🐍 backend   | build local      | ./backend     | API Flask conectada ao banco                     |
| ⚛️ frontend  | build local      | ./frontend    | React + NGINX (serve SPA e proxy para o backend) |

- O NGINX dentro do container do frontend entrega o build React e faz proxy para o backend nas rotas `/api`.
- Todos os containers estão na mesma rede Docker, permitindo comunicação direta entre os serviços pelos nomes.

---

## 🚀 Subindo o Projeto

Pré-requisitos: **Docker** e **Docker Compose v2+**

```bash
docker compose up --build
```

- Frontend disponível em: [http://localhost](http://localhost)
- Backend acessível via: [http://localhost/api](http://localhost/api) (proxy do NGINX)

---

## 🔄 Atualizando/Trocando Imagens

Sempre que houver alteração no código, reconstrua apenas o serviço necessário:

- **Atualizar tudo:**  
  ```bash
  docker compose up --build
  ```
- **Atualizar só o backend:**  
  ```bash
  docker compose up --build backend
  ```
- **Atualizar só o frontend (React/NGINX):**  
  ```bash
  docker compose up --build frontend
  ```
- **Atualizar só o banco (upgrade de versão):**  
  ```bash
  docker compose up --build db
  ```

O Compose só recria e faz deploy do serviço alterado, mantendo os demais inalterados.

---

## 📈 Escalando o Backend

Para rodar múltiplos containers do backend e suportar mais requisições:

```bash
docker compose up --scale backend=3 --build
```

- Substitua `3` pelo número de instâncias desejado.
- O NGINX no frontend distribui as requisições `/api` entre as instâncias pela rede Docker.

---

## 🧹 Limpeza Total

Para parar tudo e remover containers e volumes:

```bash
docker compose down -v
```

---

## 📚 Notas sobre o Projeto

Este repositório foi adaptado e dockerizado a partir do projeto original:  
🔗 https://github.com/fams/guess_game

Para mais informações consulte o arquivo README.md.org

---

## 📝 Licença

Distribuído sob a licença MIT.  
Veja o arquivo `LICENSE` para mais detalhes.
