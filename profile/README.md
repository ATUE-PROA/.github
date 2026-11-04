<div align="center">

![ATUE — conformidade que se comprova](./atue-banner.webp)

**Conformidade digital para empresas que não têm um departamento jurídico inteiro.**

</div>

Pequenas e médias empresas precisam provar conformidade para fechar contratos, responder a clientes e passar por auditorias — mas raramente têm time para isso. O resultado é o de sempre: política desatualizada numa pasta, evidência espalhada em e-mail, e a sensação de que o risco só aparece na hora errada.

O ATUE existe para mudar isso. Ele lê a superfície pública do site da empresa, traduz o que encontra em riscos concretos de LGPD e segurança da informação e organiza o que precisa ser feito em um fluxo único. No fim, conformidade deixa de ser um susto e vira um argumento comercial.

## Como funciona

1. **Avalia** — a empresa informa o domínio e recebe uma leitura inicial dos riscos.
2. **Organiza** — políticas, evidências e pendências ficam em um só lugar, com prioridade.
3. **Comprova** — a conformidade é apresentada com clareza para clientes, parceiros e auditorias.

## Como está desenhado

```text
atue-web ──▶ atue-core-api ──▶ atue-crawler-service
                    ├────────▶ atue-ai-service
                    └────────▶ atue-doc-service
```

Cada serviço tem uma responsabilidade clara e nenhum deles tenta ser mais inteligente do que precisa:

- **atue-core-api** — o orquestrador. Fonte única de verdade, multi-tenancy por organização, autenticação JWT e persistência em SQL Server.
- **atue-crawler-service** — inspeção stateless da superfície pública do site. Devolve o que observou; não opina.
- **atue-ai-service** — o ponto mais delicado do sistema. A classificação de risco é determinística, em catálogo fechado; o LLM local escreve apenas o resumo executivo. Risco, artigo da LGPD e recomendação nunca são inventados pelo modelo.
- **atue-doc-service** — gera os PDFs a partir de templates e entrega por URL presignada. O arquivo nunca é servido direto pela API.
- **atue-web** — a SPA em React e TypeScript que amarra tudo isso numa experiência que um não-especialista consegue usar.

## Onde está o código

| Repositório | O que tem lá |
| --- | --- |
| [atue-web](https://github.com/ATUE-PROA/atue-web) | Frontend: landing, cadastro, envio de documentos, planos e dashboard. |
| [atue-apresentation](https://github.com/ATUE-PROA/atue-apresentation) | Demonstração estática do fluxo de análise de conformidade. |

Os serviços de backend seguem privados durante o MVP. Cada repositório documenta como rodar o projeto e as convenções de engenharia que seguimos.

## Stack

React 19, TypeScript e Tailwind no frontend; ASP.NET Core (.NET 10) e SQL Server no core; Go no crawler; Python e FastAPI na camada de IA; Docker e armazenamento compatível com S3 na infraestrutura.

## Status

MVP em desenvolvimento para o Demoday. A versão atual usa dados simulados: nenhuma conta real é criada, nenhum arquivo é armazenado e não há cobrança.
