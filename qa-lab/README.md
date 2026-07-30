# QA Lab — Portal de prática para Quality Assurance

Ambiente estático (HTML/CSS/JS puro, sem build) para praticar QA de ponta a ponta: uma aplicação fake com bugs propositais e um gerenciador de casos de teste para planejar, executar e rastrear defeitos.

## Estrutura

```
qa-lab/
├── index.html            # Portal / página inicial
├── app-teste.html        # TechCart Store — sistema sob teste (contém bugs propositais)
├── casos-de-teste.html   # Gerenciador de casos de teste + log de bugs (dados no localStorage)
└── README.md
```

## Como rodar localmente

Não precisa de servidor nem instalação. Duas opções:

1. Abra `index.html` diretamente no navegador, **ou**
2. Rode um servidor estático simples (recomendado, evita restrições de `file://`):
   ```bash
   python3 -m http.server 8080
   # depois acesse http://localhost:8080
   ```

## Como publicar no GitHub Pages

1. Crie um repositório no GitHub e envie esta pasta como raiz do repositório:
   ```bash
   git init
   git add .
   git commit -m "QA Lab: portal de prática para Quality Assurance"
   git branch -M main
   git remote add origin https://github.com/SEU_USUARIO/qa-lab.git
   git push -u origin main
   ```
2. No repositório, vá em **Settings → Pages**.
3. Em "Build and deployment", selecione **Deploy from a branch**, branch `main`, pasta `/ (root)`.
4. Salve. Em alguns minutos o site estará em `https://SEU_USUARIO.github.io/qa-lab/`.

## Como usar no seu dia a dia de QA

1. **Explore** o `app-teste.html` como se estivesse homologando uma release: teste login, cadastro, busca e carrinho.
2. **Planeje** casos de teste em `casos-de-teste.html`. Use o checklist de referência (dentro da página) como ponto de partida — ele te dá cenários para pensar, não as respostas.
3. **Execute** cada caso manualmente e registre o resultado obtido. Marque o status (Passou / Falhou / Bloqueado).
4. **Reporte bugs** a partir de um caso que falhou — o botão "Reportar bug" já vincula o caso ao defeito.
5. **Evolua** a suíte: revise prioridades, quebre casos grandes em menores, mantenha o dashboard saudável.

Os dados dos casos de teste e bugs ficam salvos no `localStorage` do seu navegador — ou seja, são por navegador/dispositivo, não sincronizam entre máquinas. Isso é intencional para manter o projeto 100% estático; veja o roadmap abaixo para evoluir isso.

## Roadmap de evolução (sugestão de próximos passos)

Esta é a espinha dorsal de um estudo progressivo — não precisa fazer tudo de uma vez:

### Nível 1 — Consolidar o manual
- [ ] Escrever pelo menos 3 casos de teste por módulo (Login, Cadastro, Busca, Carrinho)
- [ ] Executar todos os casos e manter o dashboard com taxa de sucesso realista
- [ ] Registrar todos os bugs encontrados com severidade e passos de reprodução

### Nível 2 — Persistência real
- [ ] Trocar `localStorage` por um backend simples (ex: Firebase, Supabase, ou uma API própria) para os dados de casos/bugs não ficarem presos ao navegador

### Nível 3 — Automação de testes de API/UI
- [ ] Escolher uma ferramenta: **Playwright** ou **Cypress** (ambas com boa curva de aprendizado)
- [ ] Automatizar primeiro os casos mais críticos (ex: login com credenciais válidas, adicionar produto ao carrinho)
- [ ] Estruturar os testes automatizados espelhando os módulos: `tests/login.spec.js`, `tests/cadastro.spec.js`, etc.

### Nível 4 — Integração contínua
- [ ] Criar um workflow de **GitHub Actions** que rode a suíte automatizada a cada push
- [ ] Publicar o relatório de execução (ex: Playwright HTML Report) como artefato do workflow

### Nível 5 — Qualidade como processo
- [ ] Adicionar testes de regressão sempre que um bug for corrigido
- [ ] Medir cobertura de módulos testados vs. não testados
- [ ] Documentar um plano de testes (test plan) formal para uma "release" fictícia

## Sobre os bugs

O `app-teste.html` contém defeitos propositais distribuídos entre login, cadastro, busca e carrinho — a ideia é que você os encontre através de testes exploratórios e de casos formais, como em um trabalho real de QA. Não há um gabarito público de propósito: é a sua prática.
