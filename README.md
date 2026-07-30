# QA Lab — Portal de prática para Quality Assurance

Ambiente estático (HTML/CSS/JS puro, sem build) para praticar QA de ponta a ponta: uma loja real para testar e um painel de chamados independente para planejar, executar e rastrear defeitos.

## Estrutura

```
qa-lab/
├── index.html       # Portal / página inicial (explica o fluxo e linka os dois produtos)
├── loja.html        # Loja TechCart — sistema sob teste (site de e-commerce, contém bugs propositais)
├── chamados.html    # Painel de chamados — quadro Kanban de QA (dados no localStorage)
└── README.md
```

`loja.html` e `chamados.html` são propositalmente dois produtos separados, com identidade visual própria — como um site de cliente e uma ferramenta interna de QA seriam na vida real.

## Como rodar localmente

Não precisa de servidor nem instalação. Duas opções:

1. Abra `index.html` diretamente no navegador, **ou**
2. Rode um servidor estático simples (recomendado, evita restrições de `file://`):
   ```bash
   py -m http.server 8080
   # depois acesse http://localhost:8080
   ```

## Como publicar no GitHub Pages

1. Envie os arquivos (`index.html`, `loja.html`, `chamados.html`, `README.md`) direto na **raiz** do repositório — não dentro de uma subpasta.
2. No repositório, vá em **Settings → Pages**.
3. Em "Build and deployment", selecione **Deploy from a branch**, branch `main`, pasta `/ (root)`.
4. Salve. Em alguns minutos o site estará em `https://SEU_USUARIO.github.io/NOME_DO_REPO/`.

## Como usar no seu dia a dia de QA

1. **Explore** a `loja.html` como se estivesse homologando uma loja real: vitrine, catálogo, carrinho, login e cadastro.
2. **Abra chamados** em `chamados.html` para cada cenário que for testar. Use o checklist de referência (dentro da própria página) como ponto de partida — ele te dá cenários para pensar, não as respostas.
3. **Execute** movendo o chamado pelo quadro: Aberto → Em andamento → e então Resolvido (se passou) ou Bug encontrado (se falhou, com severidade).
4. **Corrija e feche**: um chamado em "Bug encontrado" vai para "Resolvido" quando você considerar o problema corrigido/retestado.
5. **Evolua** o painel: revise prioridades, quebre chamados grandes em menores, mantenha o dashboard saudável.

Os dados do painel de chamados ficam salvos no `localStorage` do seu navegador — ou seja, são por navegador/dispositivo, não sincronizam entre máquinas. Isso é intencional para manter o projeto 100% estático; veja o roadmap abaixo para evoluir isso.

## Roadmap de evolução (sugestão de próximos passos)

Esta é a espinha dorsal de um estudo progressivo — não precisa fazer tudo de uma vez:

### Nível 1 — Consolidar o manual
- [ ] Abrir pelo menos 3 chamados por módulo (Login, Cadastro, Busca, Carrinho)
- [ ] Executar todos os chamados e manter o dashboard com taxa de resolução realista
- [ ] Classificar corretamente a severidade de todo bug encontrado

### Nível 2 — Persistência real
- [ ] Trocar `localStorage` por um backend simples (ex: Firebase, Supabase, ou uma API própria) para os chamados não ficarem presos ao navegador

### Nível 3 — Automação de testes de API/UI
- [ ] Escolher uma ferramenta: **Playwright** ou **Cypress** (ambas com boa curva de aprendizado)
- [ ] Automatizar primeiro os cenários mais críticos (ex: login com credenciais válidas, adicionar produto ao carrinho)
- [ ] Estruturar os testes automatizados espelhando os módulos: `tests/login.spec.js`, `tests/cadastro.spec.js`, etc.

### Nível 4 — Integração contínua
- [ ] Criar um workflow de **GitHub Actions** que rode a suíte automatizada a cada push
- [ ] Publicar o relatório de execução (ex: Playwright HTML Report) como artefato do workflow

### Nível 5 — Qualidade como processo
- [ ] Adicionar testes de regressão sempre que um bug for corrigido
- [ ] Medir cobertura de módulos testados vs. não testados
- [ ] Documentar um plano de testes (test plan) formal para uma "release" fictícia

## Sobre os bugs

A `loja.html` contém defeitos propositais distribuídos entre login, cadastro, busca e carrinho — a ideia é que você os encontre através de testes exploratórios e de chamados formais, como em um trabalho real de QA. Não há um gabarito público de propósito: é a sua prática.
