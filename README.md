# AppMonitor Pipeline

Este repositório contém os workflows de CI/CD para o projeto AppMonitor,
focado em demonstrar as melhores práticas de automação com GitHub Actions.

## O Papel do Git na Entrega Contínua (CI/CD)

O Git é a fundação de um pipeline de CI/CD moderno. Ele atua como a **única fonte da verdade** para o código-fonte e a configuração da automação. Através dele, conseguimos:

- **Rastreabilidade:** Cada alteração é registrada em um commit, permitindo saber quem alterou o quê e por quê.
- **Automação por Eventos:** Ferramentas como o GitHub Actions usam eventos do Git (ex: `push`, `pull_request`) como gatilhos para iniciar os pipelines de build, teste e deploy.
- **Colaboração Segura:** O trabalho em paralelo é organizado de forma segura e eficiente.

### A Importância de Branches e Tags

- **Branches:** Permitem que desenvolvedores trabalhem em novas funcionalidades (`feature-branches`) ou correções (`hotfix-branches`) de forma isolada, sem afetar a estabilidade da linha de desenvolvimento principal (`main`). Pull Requests garantem a revisão do código antes da integração.

- **Tags:** São marcadores fixos em um ponto específico da história do Git, usadas para sinalizar versões de lançamento (ex: `v1.0.0`, `v1.1.0`). Elas garantem que possamos identificar e, se necessário, restaurar uma versão exata do software que foi para produção.