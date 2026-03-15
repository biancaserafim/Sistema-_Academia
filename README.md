# GymControl

Sistema de gerenciamento de academia.

**Interface:** HTML + CSS — sem alterações visuais
**Lógica/Backend:** Linguagem C pura — sockets, CRUD, arquivos binários

---

## Estrutura do projeto

```
gymcontrol/
│
├── src/                    ← Todo o código C
│   ├── main.c              ← Ponto de entrada (inicia o servidor)
│   ├── server.c            ← Servidor HTTP em C puro (sockets)
│   ├── routes.c            ← Roteador: mapeia URL → função C
│   ├── gymcontrol.h        ← Header: structs, enums, protótipos
│   ├── alunos.c            ← CRUD de alunos
│   ├── professores.c       ← CRUD de professores
│   ├── turmas.c            ← CRUD de turmas + cálculo de vagas
│   ├── fichas.c            ← CRUD de fichas de treino
│   ├── agenda.c            ← CRUD de agenda de aulas
│   ├── json_parser.c       ← Parser JSON minimalista
│   └── utils.c             ← Helpers: IDs, datas, status
│
├── data/                   ← Dados persistidos (gerado automaticamente)
│   ├── alunos.dat
│   ├── professores.dat
│   ├── turmas.dat
│   ├── fichas.dat
│   └── agenda.dat
│
├── public/                 ← Interface web (HTML + CSS intactos)
│   ├── login.html
│   ├── dashboard.html
│   ├── alunos.html
│   ├── professores.html
│   ├── turmas.html
│   ├── controle.html
│   ├── fichas.html
│   ├── style.css           ← CSS original, sem alterações
│   └── gymcontrol.js       ← Conecta HTML ↔ backend C via fetch
│
└── README.md
```



## Arquitetura (resumo para o trabalho)

```
┌─────────────────────┐        HTTP/JSON        ┌──────────────────────────┐
│   Interface Web     │ ◄──────────────────────► │   Backend em C           │
│                     │                          │                          │
│  HTML  → estrutura  │   GET /api/alunos        │  server.c  → sockets     │
│  CSS   → visual     │   POST /api/turmas       │  routes.c  → roteador    │
│  JS    → fetch()    │   DELETE /api/fichas?id= │  alunos.c  → CRUD + .dat │
│                     │                          │  turmas.c  → vagas       │
│  public/            │                          │  fichas.c  → exercícios  │
└─────────────────────┘                          └──────────────────────────┘
                                                           │
                                                    data/*.dat
                                               (arquivos binários)
```
