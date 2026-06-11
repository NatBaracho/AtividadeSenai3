# AtividadeSenai3
# Atividade Senai 3

## Visão geral

Este projeto é uma atividade de banco de dados e API para gerenciar playlists, músicas e usuários usando SQL Server.

## Arquivos do projeto

- `Banco.sql` - script de criação das tabelas no SQL Server.
- `DER.txt` - diagrama Entidade-Relacionamento e descrição das tabelas.
- `http.json` - exemplos de requisições HTTP para a API.

## Modelo de dados

Tabelas principais:

- `USUARIO`
  - `ID` INT IDENTITY(1,1) PRIMARY KEY
  - `IDADE` INT NOT NULL
  - `CPF` VARCHAR(15) NOT NULL UNIQUE

- `MUSICA`
  - `ID` INT IDENTITY(1,1) PRIMARY KEY
  - `TITULO` VARCHAR(150)
  - `ARTISTA` VARCHAR(100)
  - `DURACAO` TIME
  - `GENERO` VARCHAR(150)

- `PLAYLIST`
  - `ID` INT IDENTITY(1,1) PRIMARY KEY
  - `NOMEPLAYLIST` VARCHAR(150)
  - `PUBLICA` BIT DEFAULT 1
  - `DATACRIACAO` DATETIME2 DEFAULT SYSUTCDATETIME()
  - `USUARIO_ID` INT NOT NULL
  - Foreign key: `USUARIO_ID` REFERENCES `USUARIO(ID)`

- `PLAYLIST_MUSICA`
  - `ID` INT IDENTITY(1,1) PRIMARY KEY
  - `PLAYLIST_ID` INT FOREIGN KEY REFERENCES `PLAYLIST(ID)`
  - `MUSICA_ID` INT FOREIGN KEY REFERENCES `MUSICA(ID)`

## API HTTP

O projeto usa uma API REST para criar e listar playlists. Os exemplos estão em `http.json`.

### Endpoints principais

- `POST /api/v1/playlist`
  - Cria uma nova playlist.
  - Exemplo de body:
    ```json
    {
      "nomePlaylist": "Nirvana",
      "publica": true,
      "usuario_id": 1
    }
    ```

- `GET /api/v1/playlists`
  - Retorna a lista de playlists.

- `PUT /api/v1/playlist/{id}`
  - Atualiza os dados de uma playlist existente.

## Observações

- Use SQL Server para executar `Banco.sql`.
- No SQL Server, `BIT` usa valores `0` ou `1`.
- `TIMESTAMP` não é tipo de data no SQL Server; por isso o projeto usa `DATETIME2`.

## Como usar

1. Importe ou execute `Banco.sql` no SQL Server.
2. Garanta que a tabela `USUARIO` tenha pelo menos um usuário para associar playlists.
3. Use o arquivo `http.json` como referência para testar a API.


