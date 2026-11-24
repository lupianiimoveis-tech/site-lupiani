# Site Lupiani Imóveis — lupianiimoveis.com.br

Guia para quem for manter este site (pessoa ou Claude). Para pedir uma alteração, basta abrir uma conversa no Claude, conectar o GitHub e dizer: "Leia o LEIA-ME.md do repositório lupiani e faça tal mudança".

## O que é
Site da Lupiani Imóveis (imóveis prontos e na planta em Barueri e Alphaville), em uma página só (`index.html`), publicado pelo GitHub Pages no domínio do arquivo `CNAME`.

Funções do site: busca única no topo (código, bairro ou empreendimento) com "Mais filtros", coleções por estilo de vida, vitrine de empreendimentos com filtros avançados (região, tipo, dormitórios, fase, valor de/até, área, entrega, incorporadora e ordenação), cards com carrossel de fotos e código do imóvel, favoritos e "vistos recentemente" (guardados no navegador do visitante), comparador (até 3), página de detalhe de cada imóvel, simulador de parcela (30% da renda), guia do comprador (FAQ), formulário de triagem e o assistente virtual **Lupi**. Todos os botões levam ao WhatsApp da imobiliária com a mensagem já preenchida.

## Onde mexer dentro do `index.html`
- **Imóveis:** no `<script>`, a lista `const D=[...]`. Cada imóvel tem estes campos: `id`, `nome`, `tipo`, `status`, `cidade`, `regiao` (Barueri/Alphaville), `local`, `maps`, `pitch`, `fatos` (ficha técnica), `tipos` (plantas), `lazer`, `preco` (valor "a partir de", em reais, ou `null` para "sob consulta"), `dorms`, `m2` ([mín, máx]), `fotos` e `plantas` (chaves de imagem), `aviso` (opcional).
- **Prontos x na planta:** um imóvel conta como **pronto** quando o `status` dele contém a palavra "Pronto" (ex.: `"status": "Pronto para morar"`). Todos os outros contam como **na planta**. As abas Todos / Na planta / Prontos do topo usam essa regra.
- **Logotipo:** o símbolo dourado do prédio está em SVG dentro do `<a class="logo">` (cabeçalho) e do `<div class="logo">` (rodapé), com o texto LUPIANI IMÓVEIS ao lado.
- **Código do imóvel:** gerado pela ordem na lista `D` (LUP-001, LUP-002…). Ao incluir imóvel novo, coloque-o no **fim** da lista para não mudar os códigos dos outros.
- **Coleções:** a lista `const COLS=[...]`. Cada coleção tem `id`, título `t`, subtítulo `s`, foto `img` (chave do `IM`) e a regra `f` que escolhe os imóveis. Coleção sem nenhum imóvel some sozinha.
- **Imagens:** o objeto `const IM={...}` guarda as fotos em base64 (JPEG ~820px). Use só imagens oficiais das incorporadoras, de preferência sem pessoas.
- **WhatsApp da imobiliária:** `const FONE='5511940172182'`. Também aparece escrito no quadro de contato e no rodapé.
- **Cabeçalho:** `<header class="top">`, com o nome LUPIANI, "Fábio Lupiani · CRECI-SP 232678-F" e o botão "Falar com o corretor".
- **Lupi (assistente):** o desenho fica nas constantes `LOOP` (rosto) e `LUPIF` (corpo inteiro), em SVG. As perguntas e respostas ficam na função `chat()`.
- **Cores e fontes:** variáveis no início do `<style>` (`--navy`, `--gold` etc.).

## Publicar uma alteração
Edite o `index.html` e faça o commit na branch `main`. O GitHub Pages publica sozinho em 1 a 2 minutos.

## Domínio (Registro.br, modo avançado)
- 4 registros **A** com nome vazio: 185.199.108.153, 185.199.109.153, 185.199.110.153 e 185.199.111.153.
- 1 registro **CNAME** `www` apontando para `<conta-do-github>.github.io`.
- Se o repositório mudar de conta no GitHub, troque o CNAME do `www` para a conta nova e confirme o domínio em Settings → Pages.

## Regras de conteúdo
- Valores "a partir de" são de referência: confirme com a tabela vigente da incorporadora antes de publicar.
- Pré-lançamentos precisam do aviso de que a incorporação ainda não foi registrada.
- Não publique depoimentos inventados.
