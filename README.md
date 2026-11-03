# perplexity-ponte

Um comando de terminal que deixa o Claude Code (ou tu) fazer uma pergunta ao Perplexity e receber a resposta com as fontes.

Serve para pesquisa web atual com citações, quando o conhecimento do modelo pode estar desatualizado.

> Estado: escrito contra a API Sonar do Perplexity, mas **ainda não testado com uma chave real**. Se falhar, abre uma issue.

## Como funciona

O script lê a chave de `~/.claude/.env`, faz um `POST` a `https://api.perplexity.ai/chat/completions` com `curl` e imprime a resposta, seguida da lista de fontes.

```
tu / Claude Code  ->  perplexity-ponte  ->  API Sonar  ->  texto + fontes
```

## Requisitos

- macOS ou Linux com `zsh`, `curl` e `jq`
- Chave da API do Perplexity (a API é paga à parte da subscrição Pro)

## Instalar

```bash
git clone https://github.com/muxima127-arch/perplexity-ponte.git
cd perplexity-ponte
install -m 755 perplexity-ponte ~/.local/bin/perplexity-ponte
```

Cria a chave em perplexity.ai (Settings, API) e guarda-a assim, com o ficheiro só teu:

```bash
echo 'PERPLEXITY_API_KEY=a_tua_chave' >> ~/.claude/.env
chmod 600 ~/.claude/.env
```

Nunca ponhas a chave no repositório nem num pedido.

## Usar

```bash
perplexity-ponte "Qual é a versão estável atual do Node.js?"
perplexity-ponte -m sonar-pro "Compara as leis de IVA para e-commerce em PT e ES"
```

- `sonar` (por omissão) é o mais barato. `sonar-pro` é mais completo e mais caro.
- Sem chave, o script diz o que falta e sai com código 3.

## Usar com o Claude Code

No `CLAUDE.md`:

> Para factos atuais com fontes, usa `perplexity-ponte "<pedido>"`. Só a pedido, porque cada pedido custa dinheiro.

## Limites

- Cada pedido é cobrado pela API. Vê os preços atuais no site do Perplexity.
- O que escreves no pedido vai para o Perplexity.

## Licença

MIT
