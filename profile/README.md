# 🌊 marola

🇬🇧 [Read in English](https://github.com/marola-dev/.github/blob/main/profile/README.en.md)

Um guia amigável para o mar perto de você: qual praia está boa para nadar hoje e qual é o melhor
horário amanhã. É feito com dados públicos, em código aberto, como ciência cidadã, e diz "sem
dados" quando não sabe.

**[marola.dev](https://marola.dev/)**: o mapa ao vivo (Florianópolis, Rio de Janeiro, Salvador) ·
**[docs.marola.dev](https://docs.marola.dev/)**: como usar e como construir o marola

## Por quê

- **Aberto e sem fins lucrativos.** Boa parte dos dados do oceano no Brasil está com quem é
  dono deles, e sem esses dados ninguém prevê qualidade da água, desastre climático ou acidente
  ambiental. Uma organização sem fins lucrativos que promete compartilhar tudo pode pedir esses
  dados; mais uma empresa não poderia.
- **Primeiro a qualidade da água.** O saneamento no Brasil está longe de resolvido, então o
  marola começa pela pergunta "dá pra entrar nessa água?". Um ranking nacional de
  balneabilidade está [em discussão](https://github.com/marola-dev/marola/discussions/676).
- **Um super app da água.** Um lugar só que te entrega a resposta, e não as ferramentas: o que a
  Sequoia chama de [services as software](https://sequoiacap.com/article/services-the-new-software).
- **Código aberto, para durar.** Com IA, o código deixou de ser o segredo. O Brasil precisa de
  projetos que durem mais que as pessoas e os governos que os começaram.
- **Parceiros, não dinheiro.** Aceitamos armazenamento, horas de GPU ou dados de empresas, com
  crédito discreto no site. Sem anúncios e sem rastreamento.

## Como é feito

Um projeto, vários repositórios pequenos: um monólito distribuído. Um plano e regras em comum
deixam os agentes de IA verem o todo, enquanto cada repositório tem os próprios testes e
releases e fixa as versões publicadas dos outros em vez de ler o código deles.

### Por que um guarda-chuva

O marola começou num repositório só. Em setembro de 2026, essa árvore única obrigava tudo a
passar pelo mesmo build: uma mudança de CSS no mapa esperava o Scala compilar, e as sessões de
agente em paralelo precisavam de mais de 30 worktrees para não pisar umas nas outras. Separar em
repositórios resolve os builds, mas perde o que o repositório único fazia melhor: um agente
enxergava o projeto inteiro de uma vez.

O guarda-chuva (umbrella) fica com as duas coisas. O [marola](https://github.com/marola-dev/marola)
não tem código, só a camada do time (planos, regras, a lista de fases, o site de docs) e cada um
dos outros repositórios como submódulo git. Clonando com `--recurse-submodules`, o projeto todo
volta a ser um diretório só, com as regras comuns na raiz e as regras de cada repositório dentro
dele. Cada repositório continua compilando, testando e lançando versões sozinho, e só conversa com
os outros por artefatos versionados que ele fixa.

A ideia é antiga: um "meta-repo" que junta vários repositórios num espaço de trabalho, como faz o
manifest do [`repo`](https://source.android.com/docs/setup/reference/repo) do Android. O marola
adotou o padrão na
[MIP-0070](https://docs.marola.dev/6-MIPs/MIP-0070-umbrella-and-polyrepo-split/) (30/09/2026),
que também lista as alternativas descartadas.

<p align="center"><img src="https://raw.githubusercontent.com/marola-dev/marola/main/docs/img/umbrella.pt-BR.svg" alt="Como os repositórios do marola dependem uns dos outros" width="760" /></p>

| Repositório | O que guarda |
|---|---|
| [marola](https://github.com/marola-dev/marola) | O guarda-chuva: planos (MIPs), regras, o site de docs, cada repositório como submódulo |
| [marola-app](https://github.com/marola-dev/marola-app) | O produto: Scala 3 + Kyo, a nota e o veto de segurança, a CLI e o servidor MCP |
| [marola-site](https://github.com/marola-dev/marola-site) | O mapa em marola.dev |
| [marola-oods](https://github.com/marola-dev/marola-oods) | O Open Ocean Data Store: um arquivo aberto de praias e qualidade da água |
| [marola-corpus](https://github.com/marola-dev/marola-corpus) | O conhecimento sobre o mar, com fontes, de onde o marola responde |
| [marola-ml](https://github.com/marola-dev/marola-ml) | Compilação de prompts, o fine-tune do marola-sea, o portão de benchmark |
| [marola-devkit](https://github.com/marola-dev/marola-devkit) | Ferramentas de desenvolvimento, hooks, workflows e o plugin do Claude Code, em comum |
| [marola-skills](https://github.com/marola-dev/marola-skills) | O catálogo de todas as skills e subagentes do Claude Code nos repositórios |
| [marola-agents](https://github.com/marola-dev/marola-agents) | O inventário de todos os agentes que o marola usa ou planeja |
| [marola-research](https://github.com/marola-dev/marola-research) | Ciência |

**Quer ajudar?** Use o mapa e avise quando ele errar, ou abra uma
[issue](https://github.com/marola-dev/marola/issues) em português ou inglês. Mais em
[Como contribuir](https://docs.marola.dev/3-Ways-of-working/CONTRIBUTING/).
