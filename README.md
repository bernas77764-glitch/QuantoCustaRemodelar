# QuantoCustaRemodelar

Simulador gratuito do custo de remodelar casas, apartamentos, escritórios e lojas em Portugal.

## Modelo de negócio
- **Particulares:** simulam grátis e pedem até 3 orçamentos.
- **Profissionais:** pagam para receber esses pedidos (perfil grátis, plano mensal de 49 €/mês ou 12–25 € por contacto).

## Estrutura
Site estático, sem compilação, pronto para GitHub Pages.

```
index.html                 página completa (estilos e script incluídos)
assets/obra-fundo.jpg      fotografia de fundo
assets/favicon.svg         ícone do separador
assets/logo/               símbolo (casa com euro) em cor e em branco
```

## Onde alterar
- **Preços de referência:** tabela `WORKS` no script de `index.html` (€/m² ou €/unidade, sem IVA, para os níveis económico, médio e premium).
- **Ajustes por região:** `REGIOES`. Idade do edifício e tipo de imóvel também têm multiplicadores.
- **Cores:** tokens CSS no topo (`--escuro`, `--ocre`, ...), com grafite e ocre.

## Por fazer
- Ligar o formulário de orçamentos a um backend (ver o comentário `Ligar aqui ao backend`), por exemplo Formspree, Supabase ou um CRM.
- Validar os preços com empreiteiros.
- Substituir a fotografia de fundo por uma versão com 1920 px ou mais.

## Publicar
Settings → Pages → Source: *Deploy from a branch* → `main` / `(root)`.
