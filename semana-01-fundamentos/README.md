# Semana 1 — Fundamentos QA + Fluxo de Desenvolvimento

## 🎯 Objetivo da semana
Entender o papel do QA no ciclo de desenvolvimento, o conceito de qualidade de software (ISO 25010) e a diferença entre **verificação** e **validação**.

## 📖 Conceitos-chave

- **Verificação**: "Estamos construindo o produto corretamente?" — o software atende às especificações escritas.
- **Validação**: "Estamos construindo o produto correto?" — o software resolve o problema real do usuário.
- **ISO 25010**: modelo de qualidade de software com características como funcionalidade, confiabilidade, usabilidade, eficiência, manutenibilidade, portabilidade e segurança.

## 🔬 Estudo de Caso: Bug de Frete na "ShopFast"

### CONTEXTO
A ShopFast é um e-commerce fictício de médio porte. O time de desenvolvimento é pequeno (4 devs), sem QA dedicado. O processo de deploy consiste em: code review por um colega → merge → deploy direto em produção, sem ambiente de homologação nem testes manuais estruturados.

### PROBLEMA
Após uma atualização na regra de cálculo de frete, clientes de algumas regiões rurais passaram a pagar até 10x mais que o valor correto. O bug só foi percebido dois dias depois, através de reclamações no suporte, e já havia gerado cancelamentos de pedidos e prejuízo à reputação da marca.

### ANÁLISE
O código foi revisado e "funcionava" para os CEPs testados manualmente pelo desenvolvedor — geralmente os mais comuns, de capitais. Não houve:
- **Partição de equivalência**: as faixas de CEP não foram agrupadas em classes de teste (capital, interior, zona rural, CEPs inválidos).
- **Análise de valor limite**: os CEPs nas bordas das faixas de cálculo (onde a fórmula de frete mudava) nunca foram testados.
- Nenhuma verificação de que a regra de negócio implementada correspondia à regra realmente pretendida pelo time de produto (falha de validação, não só de verificação).

### SOLUÇÃO
- Implementar um checklist de QA obrigatório antes de qualquer deploy que envolva regras de cálculo/preço.
- Criar casos de teste específicos de valor limite para cada faixa de CEP.
- Adicionar um ambiente de homologação com dados representativos de todas as regiões atendidas.
- Envolver o QA (ou alguém com esse papel) desde a definição da regra, não só na checagem final do código.

### LIÇÃO
Um código pode passar na revisão e "funcionar" nos testes do desenvolvedor (verificação) e, mesmo assim, causar um problema grave porque a regra de negócio testada não cobria os cenários reais dos usuários (falha de validação). Qualidade não é sobre o código estar certo — é sobre o produto certo estar sendo entregue.

## 📦 Entregável
Mapa mental do fluxo de desenvolvimento com os pontos onde o QA deveria atuar — ver `mapa-mental-fluxo-qa.mermaid` nesta pasta.
