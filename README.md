### APIs HTTP públicas para integração com dados do Free Fire

> Documentação dos endpoints HTTP do projeto para integração com aplicações, bots e sistemas próprios.

As rotas usam `GET`, salvo `/ClanJoin` e `/ClanQuit`, que aceitam `GET` e `POST`. Para credenciais, tokens e senhas, prefira `POST` com corpo JSON sempre que a rota aceitar; evite expor esses valores em URLs, histórico do navegador, logs ou mensagens.

---

## Regiões suportadas

As regiões configuradas no projeto são:

```text
BD • BR • CIS • EU • ID • IND • ME • NA • PK • RU • SAC • SG • TH • TW • US • VN
```

---

## 1. Info do jogador

Consulta o perfil público de uma conta através do UID e da região.

```http
GET https://freefireapis.lat/GetPlayer?uid=228159683&region=BR&formatar=true
```

### Parâmetros

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `uid` | `string` numérica | Sim | UID da conta do jogador. |
| `region` | `string` | Sim | Região da conta, por exemplo `BR`, `NA` ou `SAC`. |
| `formatar` | `boolean` | Não | Formata datas e números para leitura. Padrão: `false`. |
| `images` | `boolean` | Não | Inclui URLs de imagens de roupa e cartão de perfil. Padrão: `false`. |
| `forceRefresh` | `boolean` | Não | Ignora o cache desta consulta e força atualização/renderização das imagens. Padrão: `false`. |

Os parâmetros booleanos aceitam `true`/`false`, `1`/`0`, `sim`/`não`, `yes`/`no` e `on`/`off`. Com `formatar=true`, campos elegíveis de data e número são apresentados em formato legível, como datas BRT e separador de milhar `.`. A disponibilidade dos blocos depende dos dados fornecidos pelo jogo.

### Resposta de sucesso

Exemplo resumido. O perfil real pode conter campos adicionais nos blocos e omitir campos sem dados.

```json
{
  "success": true,
  "result": {
    "basicInfo": {
      "accountId": "228159683",
      "nickname": "NOME_DO_JOGADOR",
      "region": "BR",
      "level": 81,
      "exp": "1.234.567",
      "rank": "Mestre",
      "rankingPoints": "2.610",
      "lastLoginAt": "24/09/2026 às 12:11:05",
      "createAt": "25/05/2019 às 17:25:07"
    },
    "clanBasicInfo": {
      "clanId": "2065877383",
      "clanName": "Root style.",
      "clanLevel": 2,
      "capacity": 25,
      "memberNum": 5
    },
    "captainBasicInfo": {
      "accountId": "552274275",
      "nickname": "NOME_DO_CAPITÃO"
    },
    "petInfo": {
      "id": 1300000112,
      "level": 4,
      "isSelected": true
    },
    "socialInfo": {
      "signature": "Assinatura do jogador"
    },
    "inventory": {
      "characterId": 102000007,
      "clothes": [],
      "weaponSkinShows": []
    }
  }
}
```

Com `images=true`, o resultado também pode incluir `clothesCard` e `profileCard`. Cada um contém URLs `png`, `jpg` e `webp`, ou um objeto de erro caso não seja possível gerar a imagem.

```json
{
  "clothesCard": {
    "png": "https://freefireapis.lat/clothes/ID_TEMPORARIO.png",
    "jpg": "https://freefireapis.lat/clothes/ID_TEMPORARIO.jpg",
    "webp": "https://freefireapis.lat/clothes/ID_TEMPORARIO.webp"
  },
  "profileCard": {
    "png": "https://freefireapis.lat/profileCard/ID_TEMPORARIO.png",
    "jpg": "https://freefireapis.lat/profileCard/ID_TEMPORARIO.jpg",
    "webp": "https://freefireapis.lat/profileCard/ID_TEMPORARIO.webp"
  }
}
```

Os links de roupa e cartão são temporários. Se expirarem, consulte o jogador novamente; use `forceRefresh=true` quando precisar forçar a atualização.

---

## 2. Info Guest

Autentica uma conta Guest e consulta informações da conta, atividade, ranks e carteira. A região é detectada durante a autenticação.

```http
GET https://freefireapis.lat/info-guest?uid=UID_GUEST&password=PASSWORD_GUEST
```

### Parâmetros

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `uid` | `string` numérica | Sim | UID da conta Guest. |
| `password` | `string` | Sim | Senha da conta Guest. |

### Resposta de sucesso

```json
{
  "success": true,
  "result": {
    "accountInfo": {
      "accountId": "14499598574",
      "accountName": "NOME_DA_CONTA",
      "region": "BR",
      "level": 20,
      "exp": "20.968"
    },
    "rankInfo": {
      "brRank": "Bronze I",
      "csRank": "Bronze I"
    },
    "activityInfo": {
      "createAt": "21/01/2026 às 16:14:29",
      "lastLoginAt": "16/09/2026 às 02:27:06"
    },
    "walletInfo": {
      "coins": "21.916",
      "gems": "50",
      "gopGems": "0",
      "totalTopup": "0",
      "lastTopupTime": "0"
    }
  }
}
```

---

## 3. Auth Guest

Autentica uma conta Guest e retorna dados básicos junto dos tokens da sessão. Os tokens são credenciais sensíveis: não os publique nem os inclua em logs ou exemplos reais.

```http
GET https://freefireapis.lat/auth-guest?uid=UID_GUEST&password=PASSWORD_GUEST
```

### Parâmetros

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `uid` | `string` numérica | Sim | UID da conta Guest. |
| `password` | `string` | Sim | Senha da conta Guest. |

### Resposta de sucesso

```json
{
  "success": true,
  "result": {
    "accountInfo": {
      "accountId": "14499598574",
      "accountName": "NOME_DA_CONTA",
      "region": "BR",
      "level": 20,
      "exp": "20.968"
    },
    "tokenInfo": {
      "openId": "<OPEN_ID>",
      "accessToken": "<ACCESS_TOKEN>",
      "jwtToken": "<JWT_TOKEN>"
    }
  }
}
```

---

## 4. History Pass

Consulta o histórico de passes pelo UID e região.

```http
GET https://freefireapis.lat/history-passe?uid=228159683&region=BR
```

### Parâmetros

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `uid` | `string` numérica | Sim | UID da conta consultada. |
| `region` | `string` | Sim | Região da conta. |

### Resposta de sucesso

```json
{
  "success": true,
  "result": {
    "Nickname": "NOME_DO_JOGADOR",
    "UID": "228159683",
    "Region": "BR",
    "Level": 81,
    "PrimeLevel": 8,
    "Language": "LANGUAGEEN",
    "ClanName": "NOME_DA_GUILD",
    "CaptainNickname": "NOME_DO_CAPITÃO",
    "CaptainUID": "552274275",
    "historyEpInfo": [
      {
        "PassEvent": 1,
        "PassLevel": 0,
        "hasElitePass": true,
        "PassNamePtBr": "Nome do passe",
        "PassNameEn": "Pass name"
      }
    ]
  }
}
```

---

## 5. Info Item ID

Consulta os dados de um item pelo ID e retorna detalhes, classificação e uma URL para a imagem PNG.

```http
GET https://freefireapis.lat/info-item?id=908046002
```

### Parâmetros

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `id` | `string` numérica | Sim | ID do item. |

### Resposta de sucesso

```json
{
  "success": true,
  "result": {
    "details": {
      "title": "Sports Car - Combust Engine",
      "itemId": 908046002,
      "iconName": "Icon_slot_Roadster_Microwaves",
      "image": "<URL_DA_IMAGEM_DO_ITEM>"
    },
    "classification": {
      "type": "COLLECTION",
      "collection": "VEHICLE_SKIN",
      "rarity": "BLUE"
    }
  }
}
```

---

## 6. Info da guilda

Consulta os detalhes de uma guilda pelo ID e região. **O parâmetro da rota é `uid`, mas nele deve ser informado o ID da guilda, não o UID de um jogador.**

```http
GET https://freefireapis.lat/GetClan?uid=2065877383&region=BR&formatar=true
```

### Parâmetros

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `uid` | `string` numérica | Sim | ID da guilda. |
| `region` | `string` | Sim | Região da guilda. |
| `formatar` | `boolean` | Não | Formata datas e números elegíveis. Padrão: `false`. |

### Resposta de sucesso

```json
{
  "success": true,
  "result": {
    "ClanID": 2065877383,
    "ClanName": "Root style.",
    "ClanCreatedAt": "16/06/2026 às 02:26:39",
    "ClanUpdatedAt": null,
    "ClanLastActive": "16/06/2026 às 02:26:57",
    "ClanLevel": 2,
    "ClanRank": 2,
    "ClanRegion": "BR",
    "ClanWelcomeMessage": "Welcome!",
    "ClanScore": "0",
    "ClanExp": "202.643",
    "ClanMembersOnline": null,
    "ClanTotalMembers": null,
    "ClanDetails": {
      "ClanSubType": "25",
      "ClanBalance": "39.999",
      "ClanUpgrades": "10",
      "ClanAchievements": "0",
      "ClanTotalPlaytime": "5.691",
      "ClanEnergy": "50"
    }
  }
}
```

Com `formatar=false`, timestamps são valores Unix e os números permanecem sem a formatação de exibição. Campos de membros podem vir como `null` quando o serviço não fornece esses dados.

---

## 7. Solicitar entrada em uma guilda

Envia uma solicitação para entrar na guilda. O servidor pode confirmar o envio da solicitação sem que isso signifique que a entrada já foi aprovada.

```http
POST https://freefireapis.lat/ClanJoin
Content-Type: application/json
```

Use **um** dos formatos de autenticação abaixo no corpo JSON.

**Conta Guest:**

```json
{
  "clan": "2065877383",
  "uid": "UID_GUEST",
  "password": "PASSWORD_GUEST"
}
```

**Token:**

```json
{
  "clan": "2065877383",
  "access_token": "<ACCESS_TOKEN_OU_JWT>"
}
```

`access_token` aceita um access token, um JWT válido ou um token EAT compatível. Não envie ao mesmo tempo `access_token` e credenciais Guest. A rota também aceita os mesmos parâmetros por query string e formulário, mas `POST` é recomendado para proteger os segredos.

### Resposta de sucesso

```json
{
  "success": true,
  "result": {
    "Action": "Join Request Sent",
    "ClanID": 2065877383,
    "AccountID": "ACCOUNT_ID",
    "AccountRegion": "BR",
    "AccountName": "NOME_DA_CONTA",
    "ClanName": "Root style.",
    "Message": "The game accepted the request; clan approval may still be required."
  }
}
```

O campo `Action` pode indicar, entre outros estados, `Join Request Sent`, `Join Request Already Pending`, `Already in Clan` ou `Joined Clan Using Guest Account`. A mensagem é retornada em inglês, conforme o contrato atual da API.

---

## 8. Sair ou cancelar uma solicitação de guilda

Envia uma ação de saída da guilda ou tenta cancelar uma solicitação pendente, conforme o estado reconhecido pelo jogo. A rota recebe os mesmos formatos de autenticação de `/ClanJoin`.

```http
POST https://freefireapis.lat/ClanQuit
Content-Type: application/json
```

**Conta Guest:**

```json
{
  "clan": "2065877383",
  "uid": "UID_GUEST",
  "password": "PASSWORD_GUEST"
}
```

**Token:**

```json
{
  "clan": "2065877383",
  "access_token": "<ACCESS_TOKEN_OU_JWT>"
}
```

### Resposta de sucesso

```json
{
  "success": true,
  "result": {
    "Action": "Left Clan Using Access Token",
    "ClanID": 2065877383,
    "AccountID": "ACCOUNT_ID",
    "AccountRegion": "BR",
    "AccountName": "NOME_DA_CONTA",
    "ClanName": "Root style.",
    "Message": "The game confirmed that the account left the clan."
  }
}
```

O valor de `Action` pode ser `Join Request Cancelled`, `Left Clan Using Guest Account`, `Left Clan Using Access Token`, entre outros. Se o perfil indicar que a conta está em outra guilda, a API não envia a solicitação de saída para evitar abandonar a guilda errada. Uma falha do jogo não é repetida automaticamente.

---

## 9. Alterar nickname

Altera o nickname da conta autenticada por credenciais Guest. Esta é uma ação que modifica a conta.

```http
GET https://freefireapis.lat/change?uid=UID_GUEST&password=PASSWORD_GUEST&name=NOVO_NICK
```

### Parâmetros

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `uid` | `string` numérica | Sim | UID da conta Guest. |
| `password` | `string` | Sim | Senha da conta Guest. |
| `name` | `string` | Sim | Novo nickname, entre 3 e 12 caracteres. |

### Resposta de sucesso

```json
{
  "success": true,
  "result": {
    "accountId": "14499598574",
    "lastLogin": "",
    "oldName": "NICK_ANTIGO",
    "newName": "NICK_NOVO",
    "region": "BR",
    "tokenLife": "success"
  }
}
```

Como essa rota atual usa `GET`, a senha pode aparecer na URL e em logs. Use-a somente em ambiente protegido; não compartilhe a URL.

---

## 10. Converter Access Token em JWT

Inspeciona um access token e retorna dados da conta e os tokens associados à sessão.

```http
GET https://freefireapis.lat/access-jwt?access_token=<ACCESS_TOKEN>
```

### Parâmetros

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `access_token` | `string` | Sim | Access token válido. |

### Resposta de sucesso

```json
{
  "success": true,
  "result": {
    "accountId": "14499598574",
    "nickname": "NOME_DA_CONTA",
    "region": "BR",
    "emulatorScore": "0",
    "isEmulator": false,
    "releaseVersion": "OB55 - 2.132.4",
    "expiresAt": "<DATA_DE_EXPIRACAO>",
    "tokenInfo": {
      "openId": "<OPEN_ID>",
      "accessToken": "<ACCESS_TOKEN>",
      "jwtToken": "<JWT_TOKEN>"
    }
  }
}
```

A resposta contém credenciais utilizáveis. Trate todos os valores em `tokenInfo` como segredos e não os armazene em documentação pública.

---

## 11. Suspensão de conta

Rota de ação sensível que envia uma solicitação ao serviço do jogo. Use somente em uma conta que você controla e em testes autorizados. O projeto atualmente aceita apenas a duração `7d`.

```http
GET https://freefireapis.lat/suspension?query=<JWT_O_ACCESS_TOKEN>&duration=7d
```

### Parâmetros

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `query` | `string` | Sim | JWT, access token ou token EAT compatível da conta alvo. |
| `duration` | `string` | Não | Duração suportada: `7d`. Padrão: `7d`. |

### Resposta de sucesso

```json
{
  "success": true,
  "result": {
    "nickname": "NOME_DA_CONTA",
    "accountId": "14499598574",
    "version": "OB55 - 2.132.4",
    "region": "BR",
    "duration": "7 days",
    "primeLevel": 0
  }
}
```

`primeLevel` pode ser omitido quando não estiver disponível. Uma resposta bem-sucedida indica que a solicitação foi aceita pelo serviço; consulte o estado da conta separadamente se precisar confirmar o resultado final.

---

## 12. Saúde e limite de requisições

### Saúde do serviço

```http
GET https://freefireapis.lat/health
```

Resposta de exemplo:

```json
{
  "success": true,
  "status": "ok",
  "uptime": 3600
}
```

`uptime` é o tempo de execução do processo em segundos.

### Estado do rate limit

```http
GET https://freefireapis.lat/rate-limit
```

Retorna um snapshot do estado agregado de rate limit, incluindo se há um limite ativo, região e etapa mais recentes, contagens e segundos desde o último evento. Não é uma consulta de perfil de jogador.

---

## 13. Rotas de imagens

As rotas de imagem retornam conteúdo binário quando a imagem existe e JSON de erro quando não está disponível. Os links de roupa e cartão são gerados por `/GetPlayer?images=true` e podem expirar; solicite o perfil novamente para obter links atuais.

- `/items/<item_id>.png`: imagem PNG de item. É a rota canônica para imagens de itens.
- `/clothes/<id_temporario>.png`, `/clothes/<id_temporario>.jpg` e `/clothes/<id_temporario>.webp`: renderização do conjunto de roupas.
- `/profileCard/<id_temporario>.png`, `/profileCard/<id_temporario>.jpg` e `/profileCard/<id_temporario>.webp`: cartão renderizado do perfil.

O campo `details.image` de `/info-item` contém o link direto da imagem do item. Os formatos `png`, `jpg` e `webp` são aceitos nas rotas `/clothes` e `/profileCard`. A geração depende dos recursos e templates disponíveis no servidor; em caso de ausência, a API pode retornar um erro específico em vez da URL.

---

## 14. Erros

As respostas de erro usam este formato JSON padrão:

```json
{
  "success": false,
  "error": "INVALID_REGION",
  "message": "Region is invalid or unsupported.",
  "solution": "Provide a valid region code."
}
```

`error` é o código estável para tratamento pelo cliente; `message` descreve o problema e `solution` sugere como corrigir. Os textos atuais são retornados em inglês. O status HTTP pode variar por endpoint, então verifique também `success` e `error`.

Códigos comuns incluem `MISSING_PARAMETERS` (parâmetro obrigatório ausente), `INVALID_UID`, `INVALID_REGION`, `INVALID_CLAN_ID` e `INVALID_ITEM_ID` (identificador inválido), `PLAYER_NOT_FOUND`, `GUILD_NOT_FOUND` e `CLAN_INFO_FAILED` (consulta sem resultado ou falha do serviço), `AUTH_FAILED`, `INVALID_TOKEN` e `INSPECTOKEN_ERROR` (autenticação/token), `RATE_LIMITED` (limite temporário), além de `ITEM_NOT_FOUND` e erros de imagem como `CLOTHES_NOT_FOUND`, `PROFILE_CARD_NOT_FOUND` e `ITEM_IMAGE_NOT_FOUND`.
