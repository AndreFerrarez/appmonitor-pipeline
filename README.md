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

---

## Variáveis, Segredos e Contextos

Um pipeline robusto precisa ser configurável sem expor dados sensíveis. O GitHub Actions oferece diferentes maneiras de gerenciar configurações:

### 1. GitHub Secrets (`secrets`)

* **Propósito:** Armazenar dados altamente sensíveis que não devem ser expostos, como chaves de API, tokens, senhas, etc.
* **Características:**
    * São **criptografados** antes de chegar ao GitHub e permanecem assim.
    * Uma vez salvos, seu valor **não pode mais ser visualizado** na interface do GitHub, apenas atualizado.
    * São **automaticamente censurados (mascarados com `***`)** nos logs do workflow se houver uma tentativa de imprimi-los.
* **Como usar:** `${{ secrets.NOME_DO_SEGREDO }}`

### 2. GitHub Variables (`vars`)

* **Propósito:** Armazenar dados de configuração não sensíveis que podem ser reutilizados em múltiplos workflows. Exemplos: nome de ambiente (`dev`, `staging`, `prod`), URLs, nomes de usuário.
* **Características:**
    * São armazenados como **texto plano**.
    * Seu valor **pode ser visualizado e editado** a qualquer momento na interface do GitHub.
    * **Não são mascarados** nos logs.
* **Como usar:** `${{ vars.NOME_DA_VARIAVEL }}`

### 3. Environment Variables (`env`)

* **Propósito:** É uma forma de **utilizar** os `secrets` e `vars` dentro do ambiente de execução do job. É uma variável de ambiente padrão, com escopo limitado ao job ou ao step onde é definida.
* **Características:** É a "ponte" entre os contextos do GitHub Actions e os scripts ou ferramentas que rodam no pipeline.