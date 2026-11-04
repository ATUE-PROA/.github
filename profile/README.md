<div align="center">

# ATUE

**Conformidade digital para pequenas e médias empresas.**

Entenda os riscos do seu site, organize evidências e comprove conformidade com a LGPD.

![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-6-3178C6?logo=typescript&logoColor=white)
![.NET](https://img.shields.io/badge/.NET-10-512BD4?logo=dotnet&logoColor=white)
![Go](https://img.shields.io/badge/Go-00ADD8?logo=go&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![SQL Server](https://img.shields.io/badge/SQL_Server-CC2927?logo=microsoftsqlserver&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)

</div>

## O que é o ATUE

O ATUE é uma plataforma B2B SaaS que ajuda pequenas e médias empresas a **entender, organizar e comprovar** sua conformidade digital. A plataforma parte de uma leitura do domínio da empresa — o que está exposto, quais requisitos de LGPD e segurança da informação estão em jogo — e transforma esse diagnóstico em documentos, evidências e pendências organizadas em um fluxo único.

O objetivo é tornar conformidade um diferencial comercial: menos surpresa em auditorias, mais transparência para clientes e parceiros.

> **Projeto em desenvolvimento para o Demoday.** A versão atual é um MVP com dados simulados: nenhuma conta real é criada, nenhum arquivo é armazenado e não há cobrança.

## Como funciona

1. **Avalia** — informe seu domínio e receba uma leitura inicial dos riscos e oportunidades.
2. **Organiza** — políticas, evidências e pendências em um fluxo simples.
3. **Comprova** — apresente sua conformidade com clareza para clientes e parceiros.

## Arquitetura

```text
atue-web ──▶ atue-core-api ──▶ atue-crawler-service
                    ├────────▶ atue-ai-service
                    └────────▶ atue-doc-service
```

- **atue-core-api** — orquestrador e fonte única de verdade: multi-tenancy por organização, autenticação JWT, persistência em SQL Server com Entity Framework Core.
- **atue-crawler-service** — worker stateless que inspeciona HTML e headers públicos de um domínio e devolve os dados brutos observados, sem regra de negócio.
- **atue-ai-service** — tradução técnico→jurídica: classifica achados em um catálogo determinístico e usa um LLM local apenas para o resumo executivo. Riscos, artigos da LGPD e recomendações nunca vêm do modelo.
- **atue-doc-service** — geração de PDFs a partir de templates e entrega por URL presignada.
- **atue-web** — SPA em React 19, TypeScript e Tailwind CSS v4.

## Repositórios públicos

| Repositório                                                                  | Descrição                                                                 |
| ---------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| [atue-web](https://github.com/ATUE-PROA/atue-web)                           | Frontend SPA: landing, cadastro, envio de documentos, planos e dashboard. |
| [atue-apresentation](https://github.com/ATUE-PROA/atue-apresentation)       | Demonstração estática do fluxo de análise de conformidade.                |

## Stack

**Frontend:** React 19 · TypeScript · Vite · Tailwind CSS v4 · shadcn/ui · React Router · Recharts

**Backend:** ASP.NET Core (.NET 10) · C# 13 · Entity Framework Core · SQL Server · Go · Python / FastAPI

**Infra:** Docker · MinIO/S3 para armazenamento de documentos

Cada repositório tem seu próprio `README.md` com instruções de execução e um `AGENTS.md` com as convenções de engenharia do projeto.
