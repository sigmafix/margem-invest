# Margem Invest

App web para celular que ajuda a montar uma carteira de investimentos com **margem de segurança**: ações do Brasil, ações dos EUA e fundos imobiliários (FIIs), com opções para curto, médio e longo prazo, e uma aba de estatísticas para entender o que está na carteira.

Roda direto no navegador, em um único arquivo (`index.html`), sem instalação e sem servidor próprio.

> **Material educativo. Não é recomendação de compra ou venda de ativos.** Confira todos os dados em fontes oficiais antes de investir.

## O que o app faz

### Aba Carteira

1. Você informa o **valor** a investir, o **prazo** (curto, médio ou longo), o **perfil de risco** (conservador, moderado ou arrojado), a **exposição ao exterior** (0 a 100% das ações) e a parcela de **FIIs** (0 a 40% da parte em ações).
2. O app dá uma **nota de 0 a 100** para cada um dos 50 ativos analisados e monta uma carteira com a parte de renda fixa do seu perfil.
3. Mostra o peso de cada ativo em um mapa de blocos, o valor em reais e, quando há preço, a **quantidade de cotas** a comprar.
4. Traz um **ranking de oportunidades** com filtros (Brasil, EUA, FIIs, favoritos) e ordenação por nota, margem de segurança, dividendo, crescimento ou menor risco.
5. Ao tocar em um ativo: nota por fator, margem de segurança pelos métodos de Graham, Lynch e Bazin, pontos fortes, pontos de atenção e campos para corrigir os indicadores.
6. O botão **Copiar carteira** gera um texto com ativos, pesos e valores.

### Aba Estatísticas

- Retorno estimado, dividendos, renda mensal estimada, P/L, ROE, margem líquida, beta, queda estimada em uma crise forte, margem de segurança média e concentração.
- **Leituras automáticas**: setor pesado, exposição ao dólar, concentração e retorno frente à renda fixa.
- Alocação por país e por setor, mapa de risco contra nota e perfil da carteira por fator.
- **Simulação de patrimônio** em três cenários (pessimista, base e otimista) contra só renda fixa, com aporte mensal e valor corrigido pela inflação.
- Panorama de Brasil, EUA e FIIs, explicação da nota e glossário.

### Extras

- Português, inglês e espanhol (abre no idioma do aparelho).
- Tema automático, claro ou escuro e 5 cores de destaque.
- Funciona bem em telas pequenas.
- As escolhas ficam salvas no navegador do aparelho.

## Como a nota é calculada

Cada ativo recebe cinco notas de 0 a 100, e a nota final é a média ponderada:

| Fator | O que mede |
| --- | --- |
| Valor | Margem de segurança: média dos métodos de Graham (lucro e patrimônio) e Lynch (crescimento e dividendos). Nos FIIs, o desconto sobre o valor patrimonial (P/VP). |
| Qualidade | ROE, margem líquida e endividamento. Nos FIIs, a vacância. |
| Crescimento | Crescimento anual do lucro. |
| Dividendos | Dividend yield. |
| Estabilidade | Beta e endividamento. |

O prazo muda os pesos:

| Prazo | Valor | Qualidade | Crescimento | Dividendos | Estabilidade |
| --- | --- | --- | --- | --- | --- |
| Curto | 35% | 15% | 10% | 25% | 15% |
| Médio | 25% | 25% | 20% | 15% | 15% |
| Longo | 15% | 30% | 30% | 10% | 15% |

O perfil de risco multiplica o peso da estabilidade (conservador valoriza mais, arrojado valoriza menos) e define a estrutura da carteira:

| Perfil | Renda fixa | Ativos | Máximo por ativo |
| --- | --- | --- | --- |
| Conservador | 30% | até 8 | 12% |
| Moderado | 15% | até 10 | 15% |
| Arrojado | 5% | até 12 | 18% |

O app evita mais de 2 ativos do mesmo setor sempre que possível.

## Dados

### Dados de referência

Os indicadores de cada ação e FII (P/L, P/VP, dividend yield, ROE, margem líquida, crescimento, dívida e beta) são **valores aproximados de referência**, embutidos no arquivo, e podem estar defasados. Você pode corrigir qualquer valor tocando no ativo. O valor digitado por você sempre tem prioridade.

### Dados ao vivo (opcional)

Quando o app é publicado em um site (como o GitHub Pages), ele busca dados ao abrir:

| Fonte | O que traz | Chave |
| --- | --- | --- |
| Banco Central (SGS) | Selic (série 432), IPCA em 12 meses (13522), dólar (1) e CDI (4389) | Não precisa |
| [brapi.dev](https://brapi.dev) | Preço das ações e FIIs do Brasil, P/L das ações do Brasil e Ibovespa | Chave gratuita |
| [Finnhub](https://finnhub.io) | Preço e indicadores das ações dos EUA | Chave gratuita |

Para ligar, abra o app, toque na engrenagem, vá em **Dados ao vivo**, cole as chaves e toque em **Salvar e atualizar**. As chaves ficam salvas só no aparelho de quem as digitou.

- Os dados são buscados de novo quando têm mais de 15 minutos. O botão **Atualizar agora** força a busca.
- O painel de Ajustes mostra o status de cada fonte, com o código do erro quando algo falha.
- Se uma fonte falhar, o app continua com os valores de referência e avisa na tela.
- Continuam de referência: P/VP, dividendos, ROE, margem, crescimento e dívida das ações do Brasil, os indicadores dos FIIs (exceto o preço) e a dívida sobre EBITDA das ações dos EUA.

> A camada de dados ao vivo foi testada com respostas simuladas. Os formatos reais e os limites dos planos gratuitos podem mudar. Confira o painel de status no primeiro uso.

## Como publicar no GitHub Pages

1. Crie um repositório **público** e envie o arquivo `index.html` (o nome precisa ser esse).
2. Em **Settings**, **Pages**, escolha **Deploy from a branch**, branch `main` e pasta `/ (root)`, e salve.
3. Aguarde alguns minutos. O endereço será `https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/`.

**Atenção com as chaves:** em um repositório público, não escreva chaves dentro do arquivo. Digite-as só nos Ajustes do app.

## Tecnologia

- Um único arquivo HTML com CSS e JavaScript puro, sem dependências nem etapa de build.
- Fontes carregadas do Google Fonts.
- Gráficos desenhados em SVG, mapa de blocos com algoritmo de treemap.

## Limitações conhecidas

- Os indicadores de referência podem estar desatualizados.
- A lista tem 50 ativos: 25 ações do Brasil, 17 dos EUA e 8 FIIs.
- O método de Graham tende a achar caras as ações de crescimento, especialmente as americanas.
- A projeção de retorno é uma estimativa simples, não uma previsão.
- O app não envia ordens a corretoras e não guarda dados em servidor.

## Aviso legal

Este projeto é educativo. Nada aqui é recomendação de investimento, oferta ou consultoria financeira. Rentabilidade passada não garante rentabilidade futura, e ativos no exterior sofrem variação cambial. Antes de investir, confira os dados em fontes oficiais e, se precisar, converse com um profissional certificado.
