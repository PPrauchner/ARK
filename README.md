<p align="center">
  <img src="assets/banner.svg" alt="ARK, Agent Rules Kit" width="100%">
</p>

<p align="center">
  <a href="README.md"><img src="https://img.shields.io/badge/idioma-português-1d4ed8?style=flat-square" alt="Português"></a>
  <a href="README.en.md"><img src="https://img.shields.io/badge/language-english-60a5fa?style=flat-square" alt="English"></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/feito_para-Claude_Code-0b1f3f?style=flat-square" alt="Feito para Claude Code">
  <img src="https://img.shields.io/badge/versão-9-1d4ed8?style=flat-square" alt="Versão 9">
  <img src="https://img.shields.io/badge/commits-200%2B-2563eb?style=flat-square" alt="Mais de 200 commits">
  <img src="https://img.shields.io/badge/ADRs-7-3b82f6?style=flat-square" alt="7 ADRs">
  <img src="https://img.shields.io/badge/linguagens-11-60a5fa?style=flat-square" alt="Convenções para 11 linguagens">
</p>

<div align="justify">

O ARK é o kit de processo que eu uso para trabalhar com o
[Claude Code](https://docs.anthropic.com/en/docs/claude-code). Ele faz o agente
seguir o mesmo caminho que eu cobraria de qualquer pessoa da equipe: partir de uma
issue, escrever o teste antes, commitar em partes pequenas, abrir PR, passar por
revisão e deixar as decisões registradas. E faz isso do mesmo jeito em todos os meus
repositórios.

</div>

> [!NOTE]
> O código do ARK é privado. Esta página conta o que ele faz e por que foi desenhado
> assim.

<h2 align="center">Por que existe</h2>

<div align="justify">

Um agente de IA escreve código rápido, mas sozinho ele não cuida do resto. Não sabe
por que a issue foi aberta, diz que algo funciona sem ter rodado os testes, junta
várias mudanças no mesmo commit e não anota as decisões que tomou. Num projeto de uma
semana isso passa despercebido. Num projeto de semestre, com equipe, vira retrabalho.

</div>

<div align="justify">

Em vez de corrigir isso em cada projeto, juntei as regras num kit só. Quando melhoro
uma delas, todos os repositórios passam a usar a versão nova, e dentro de cada
projeto fica só o que é específico dele.

</div>

<h2 align="center">Como o trabalho anda</h2>

```mermaid
flowchart LR
    A([Issue pronta]) --> B[Implementação<br/>com TDD]
    B --> C[Commits<br/>atômicos]
    C --> D[Pull request]
    D --> E{Revisão}
    E -- ajustes --> B
    E -- aprovado --> F[Branch de<br/>integração]
    F --> G((Merge no tronco<br/>por uma pessoa))

    classDef step fill:#dbeafe,stroke:#1d4ed8,stroke-width:2px,color:#0b1f3f
    classDef gate fill:#1d4ed8,stroke:#0b1f3f,stroke-width:2px,color:#ffffff
    classDef human fill:#0b1f3f,stroke:#38bdf8,stroke-width:3px,color:#ffffff
    class A,B,C,D,F step
    class E gate
    class G human
```

<div align="justify">

Cada etapa pode ser usada sozinha, com alguém acompanhando. O `/exhaust` junta todas:
pega a fila de issues prontas, na ordem de prioridade, e leva uma por uma até o
merge. Ele implementa, abre o PR, revisa, corrige e mergeia sem ninguém olhando. Só
não mergeia no tronco. Essa decisão continua sendo de uma pessoa.

</div>

<h2 align="center">Decisões de design</h2>

<div align="justify">

Quando o `/exhaust` trabalha sozinho, o merge vai para uma branch de integração
separada, que pode ser jogada fora inteira. Se um erro escapar da revisão na primeira
issue, ele não chega ao projeto principal antes de alguém olhar.

</div>

<div align="justify">

A revisão olha duas coisas diferentes: se o PR faz o que a issue pede, respeitando o
que já foi decidido no projeto, e se o código em si está bom. Cada pergunta tem um
revisor próprio, e o critério de cada um está escrito num lugar só. Já aconteceu de a
mesma regra existir copiada em mais de um comando, e as cópias acabaram ficando diferentes.

</div>

<div align="justify">

Nenhum commit feito sem supervisão entra com teste falhando. E antes de implementar,
o agente lê o glossário do projeto e os registros de decisão (ADRs), que é onde fica
o porquê de cada escolha.

</div>

<h2 align="center">Onde já foi usado</h2>

<div align="justify">

Uma versão inicial do ARK organizou o trabalho da equipe de seis pessoas do
[SAGA](https://github.com/PPrauchner/SAGA-Sistema-de-Acompanhamento-e-Gestao-Academica),
um sistema de gestão para programas de pós-graduação. Desde então ele chegou à
versão 9.

</div>

<h2 align="center">Créditos</h2>

<div align="justify">

Algumas skills de apoio, como `tdd`, `grill-me` e `triage`, vêm do
[mattpocock/skills](https://github.com/mattpocock/skills), sob licença MIT. Os
princípios de comportamento do agente partem do
[multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills).
O fluxo, os agentes, as regras e as decisões de arquitetura são meus.

</div>

<h2 align="center">Contato</h2>

<p align="center">O ARK segue em desenvolvimento. Também ajudo equipes pequenas a montar esse fluxo nos repositórios delas. Se faz sentido para a sua, me chama no LinkedIn.</p>

<p align="center">
  <a href="mailto:pietro.mprauchner@gmail.com"><img src="https://img.shields.io/badge/e--mail-pietro.mprauchner%40gmail.com-1d4ed8?style=flat-square&logo=gmail&logoColor=white" alt="E-mail"></a>
  <a href="https://github.com/PPrauchner"><img src="https://img.shields.io/badge/github-PPrauchner-0b1f3f?style=flat-square&logo=github&logoColor=white" alt="GitHub"></a>
  <a href="https://www.linkedin.com/in/pietroprauchner/"><img src="https://img.shields.io/badge/linkedin-pietroprauchner-2563eb?style=flat-square" alt="LinkedIn"></a>
</p>
