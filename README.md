### APIs HTTP públicas para integração com dados do Free Fire

> Documentação dos endpoints HTTP públicos para Free Fire, criada para facilitar a integração com aplicações, bots e sistemas próprios. Consulte endpoints, parâmetros, exemplos de requisições, respostas em JSON e mensagens retornadas pela API.
---

## Regiões suportadas

Atualmente, as APIs possuem suporte para **16 regiões** do Free Fire:

```text
BR • SAC • US • NA • IND • BD • ID • ME • VN • TH • CIS • RU • PK • SG • EU • TW
```
---

## 1. Info do jogador

Consulta informações públicas de uma conta do Free Fire através do UID e da região.

```http
GET https://freefireapis.lat/info-player?uid=228159683&region=BR
```

### Parâmetros

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `uid` | `string` | Sim | UID da conta do jogador |
| `region` | `string` | Sim | Região da conta |

### Resposta de sucesso

```json
{
  "success": true,
  "result": {
    "clothesUrl": {
      "png": "https://freefireapis.lat/clothes/m4s-YhpW5a.png",
      "jpg": "https://freefireapis.lat/clothes/m4s-YhpW5a.jpg",
      "webp": "https://freefireapis.lat/clothes/m4s-YhpW5a.webp"
    },
    "infoUrl": null,
    "basicInfo": {
      "accountId": "1033857091",
      "accountType": 1,
      "nickname": "@HubsGGxㅤꚠ",
      "primeLevel": 4,
      "region": "BR",
      "language": "LANGUAGEINDONESIAN",
      "level": 72,
      "exp": "3.695.922",
      "bannerId": 901042013,
      "headPic": 902000330,
      "rank": "Platina V",
      "rankingPoints": "2.610",
      "hasElitePass": true,
      "badgeCnt": "8",
      "badgeId": 1001000100,
      "seasonId": 53,
      "liked": "53.673",
      "showRank": true,
      "lastLoginAt": "24/09/2026 às 12:11:05",
      "csRank": "Mestre",
      "csRankingPoints": "89",
      "maxRank": "Platina V",
      "csMaxRank": "Mestre",
      "createAt": "25/05/2019 às 17:25:07",
      "title": 904090027,
      "releaseVersion": "OB55",
      "showBrRank": true,
      "showCsRank": true,
      "hippoRank": 14,
      "hippoRankingPoints": "19",
      "csPeakTournamentRankPos": "1.363",
      "avatarFrame": 1,
      "brPointsToNextRank": 140,
      "csPointsToNextRank": 3711,
      "brPointsRate": "34.0",
      "csPointsRate": "0.0",
      "xpInfo": {
        "levelText": "Conta level 72",
        "currentInLevel": "323.638",
        "totalInLevel": "327.171",
        "toNextLevel": "3.533",
        "rate": "98.9"
      }
    },
    "clanBasicInfo": {
      "clanId": "2065877383",
      "clanName": "Root style.",
      "captainId": "1033857091",
      "clanLevel": 2,
      "capacity": 25,
      "memberNum": 5
    },
    "captainBasicInfo": {
      "accountId": "1033857091",
      "accountType": 1,
      "nickname": "@HubsGGxㅤꚠ",
      "primeLevel": 4,
      "region": "BR",
      "language": "LANGUAGEINDONESIAN",
      "level": 72,
      "exp": "3.695.922",
      "bannerId": 901042013,
      "headPic": 902000330,
      "rank": "Platina V",
      "rankingPoints": "2.610",
      "hasElitePass": true,
      "badgeCnt": "8",
      "badgeId": 1001000100,
      "seasonId": 53,
      "liked": "53.673",
      "showRank": true,
      "lastLoginAt": "24/09/2026 às 12:11:05",
      "csRank": "Mestre",
      "csRankingPoints": "89",
      "maxRank": "Platina V",
      "csMaxRank": "Mestre",
      "createAt": "25/05/2019 às 17:25:07",
      "title": 904090027,
      "releaseVersion": "OB55",
      "showBrRank": true,
      "showCsRank": true,
      "hippoRank": 14,
      "hippoRankingPoints": "19",
      "csPeakTournamentRankPos": "1.363",
      "avatarFrame": 1,
      "brPointsToNextRank": 140,
      "csPointsToNextRank": 3711,
      "brPointsRate": "34.0",
      "csPointsRate": "0.0"
    },
    "petInfo": {
      "id": 1300000112,
      "level": 4,
      "exp": "540",
      "isSelected": true,
      "skinId": 1310000121,
      "selectedSkillId": 1315000014
    },
    "socialInfo": {
      "accountId": "1033857091",
      "language": "LANGUAGEARABIC",
      "signature": "[b][FFFF00]@HubsGGx[b] [FF0000]Desenvolvedor de Software focado na criação de bots, APIs e sistemas backend escaláveis, com experiência em automação e soluções web modernas. ϟ",
      "rankShow": "RANKSHOWBR"
    },
    "creditScoreInfo": {
      "creditScore": 100,
      "rewardState": "REWARDSTATEUNCLAIMED",
      "periodicSummaryEndTime": "23/09/2026 às 16:15:31",
      "periodicSummaryLevel": 1790450131
    },
    "userSparkInfo": {
      "state": "SparkState_ACTIVE",
      "level": 22500
    },
    "inventory": {
      "characterId": 102000007,
      "characterName": "Maxim",
      "characterImage": "https://freefireapis.lat/image/102000007.png",
      "clothes": [
        {
          "title": "Commando (Pants)",
          "id": 204000143,
          "collection": "NONE",
          "rarity": "PURPLE",
          "type": "Clothes",
          "image": "https://freefireapis.lat/image/204000143.png"
        },
        {
          "title": "Bandit (Top)",
          "id": 203000449,
          "collection": "NONE",
          "rarity": "ORANGE",
          "type": "Clothes",
          "image": "https://freefireapis.lat/image/203000449.png"
        },
        {
          "title": "Woof Pro Catcher (Head)",
          "id": 211000567,
          "collection": "NONE",
          "rarity": "PURPLE",
          "type": "Clothes",
          "image": "https://freefireapis.lat/image/211000567.png"
        },
        {
          "title": "Aero Flex (Shoes)",
          "id": 205046025,
          "collection": "NONE",
          "rarity": "PURPLE",
          "type": "Clothes",
          "image": "https://freefireapis.lat/image/205046025.png"
        },
        {
          "title": "Sonic Eyes Facepaint",
          "id": 214035012,
          "collection": "NONE",
          "rarity": "PURPLE_PLUS",
          "type": "Clothes",
          "image": "https://freefireapis.lat/image/214035012.png"
        },
        {
          "title": "Iron Blade (Mask)",
          "id": 211000164,
          "collection": "NONE",
          "rarity": "PURPLE",
          "type": "Clothes",
          "image": "https://freefireapis.lat/image/211000164.png"
        }
      ],
      "weaponSkinShows": [
        {
          "title": "UMP - Cataclysm",
          "id": 907001503,
          "collection": "WEAPON_SKIN",
          "rarity": "PURPLE",
          "type": "Weapon Skin",
          "image": "https://freefireapis.lat/image/907001503.png"
        },
        {
          "title": "Wrath of the Nine Tails",
          "id": 912047002,
          "collection": "GROUPANIM",
          "rarity": "ORANGE",
          "type": "Weapon Skin",
          "image": "https://freefireapis.lat/image/912047002.png"
        },
        {
          "title": "Naruto's Ascent Look Changer",
          "id": 914047001,
          "collection": "TRANSFORM_EMOTE",
          "rarity": "RED",
          "type": "Weapon Skin",
          "image": "https://freefireapis.lat/image/914047001.png"
        }
      ]
    }
  }
}
```

---

## 2. Info Guest

Consulta informações de uma conta Guest através do UID e da senha, incluindo informações de banimento e carteira.

```http
GET https://freefireapis.lat/info-guest?uid=UID_GUEST&password=PASSWORD_GUEST
```

### Parâmetros

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `uid` | `string` | Sim | UID da conta Guest |
| `password` | `string` | Sim | Senha da conta Guest |

### Resposta de sucesso

```json
{
  "success": true,
  "result": {
    "accountInfo": {
      "accountId": "14499598574",
      "accountName": "M4S-GVDJYbPG",
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

Autentica uma conta Guest através do UID e da senha e retorna informações básicas da conta, além dos tokens de autenticação associados à sessão.

### Requisição

```http
GET https://freefireapis.lat/auth-guest?uid=UID_GUEST&password=PASSWORD_GUEST
```

### Parâmetros

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `uid` | `string` | Sim | UID da conta Guest que será autenticada |
| `password` | `string` | Sim | Senha da conta Guest |

### Resposta de sucesso

```json
{
  "success": true,
  "result": {
    "accountInfo": {
      "accountId": "14499598574",
      "accountName": "M4S-GVDJYbPG",
      "region": "BR",
      "level": 20,
      "exp": "20.968"
    },
    "tokenInfo": {
      "openId": "8d7a0977e75c7ef35e426074eaf7f343...",
      "accessToken": "340b73afc547b1f677020a90cc2...",
      "jwtToken": "eyJhbGciOiJIUzI1NiIsInN2ciI6IjIi..."
    }
  }
}
```
---
## 4. History Pass

Consulta o histórico de passes de uma conta através do UID e da região. Retorna informações básicas do usuário, incluindo o **Level**, além do histórico dos eventos de passe e a indicação de quais passes possuem **Elite Pass**.

### Requisição

```http
GET https://freefireapis.lat/history-pass?uid=UID&region=REGION
```

### Parâmetros

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `uid` | `string` | Sim | UID da conta que será consultada |
| `region` | `string` | Sim | Região da conta, como `BR`, `NA`, `SAC`, `IND`, etc. |

### Resposta de sucesso

```json
{
  "success": true,
  "result": {
    "Nickname": "PAPAIㅤD0ㅤANO",
    "UID": "228159683",
    "Region": "BR",
    "Level": 81,
    "PrimeLevel": 8,
    "Language": "LANGUAGEEN",
    "ClanName": "FLUXOㅤW7M",
    "CaptainNickname": "FXㅤALE10.YTㅤ",
    "CaptainUID": "552274275",
    "historyEpInfo": [
      {
        "PassEvent": 1,
        "PassLevel": 0,
        "hasElitePass": true,
        "PassNamePtBr": "Sakura",
        "PassNameEn": "Sakura"
      },
      {
        "PassEvent": 2,
        "PassLevel": 0,
        "hasElitePass": true,
        "PassNamePtBr": "Hip Hop",
        "PassNameEn": "Hip Hop"
      }
    ]
  }
}
```
---
## 5. Info Item ID

Consulta informações de um item do Free Fire através do ID, retornando detalhes como **título, ícone, imagem, tipo, coleção e raridade**.

### Requisição

```http
GET https://freefireapis.lat/info-item?id=908046002
```

### Parâmetros

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `id` | `string` | Sim | ID do item que deseja consultar. |

### Resposta de sucesso

```json
{
  "success": true,
  "result": {
    "details": {
      "title": "Sports Car - Combust Engine",
      "itemId": 908046002,
      "iconName": "Icon_slot_Roadster_Microwaves",
      "image": "https://freefireapis.lat/image/908046002.png"
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
