# QuantoCustaRemodelar · Resumo do projeto

Documento para recuperar o projeto noutra conta (por exemplo, Claude Teams). Reúne o que foi feito, as decisões tomadas, onde está cada ficheiro e o que falta fazer.

Última atualização: 3 de novembro de 2026.

---

## 1. Onde está tudo

| O quê | Onde | Notas |
|---|---|---|
| **Código do site (fonte principal)** | https://github.com/bernas77764-glitch/QuantoCustaRemodelar (ramo `main`) | Repositório público e independente do MM Detalhe. É isto que importa guardar. |
| **Site online** | https://bernas77764-glitch.github.io/QuantoCustaRemodelar/ | GitHub Pages, publica sozinho a cada alteração no `main`. |
| Pré-visualização do site no Claude | https://claude.ai/artifact/NuZkFdQyWaKpUJyXPKGxSo | Ligada à conta pessoal. Pode deixar de estar acessível depois da migração. |
| Estudo de logótipos no Claude | https://claude.ai/artifact/Ub9rBAhJdYcL2ES85rhgKH | Também está no repositório: `docs/estudo-logotipos.html`. |

O repositório no GitHub não depende da conta Claude. Mudar para o Claude Teams não apaga nada no GitHub.

### Ficheiros do repositório

```
index.html                     site completo (HTML, CSS e JavaScript num só ficheiro)
404.html                       página "Esta página não existe"
assets/obra-fundo.jpg          fotografia de fundo (trabalhador a rebocar, 770×512 px)
assets/favicon.svg             ícone do separador (casa com €)
assets/logo/simbolo-cor.svg    logótipo: casa grafite com € ocre
assets/logo/simbolo-branco.svg logótipo para fundos escuros: casa branca com € ocre
docs/estudo-logotipos.html     as 6 propostas de logótipo estudadas
README.md                      instruções curtas
PROJETO.md                     este documento
.nojekyll                      necessário para o GitHub Pages
```

---

## 2. O conceito

Site para particulares simularem o custo de remodelar uma casa, apartamento, escritório ou loja em Portugal, seguindo o modelo de negócio do QuantoCustaCasar:

- **Particulares:** simulam grátis, sem registo, e podem pedir até 3 orçamentos.
- **Profissionais (quem paga):** recebem esses pedidos já com a simulação completa (área, obras, acabamentos, região, prazo). Planos propostos:
  - **Perfil grátis:** 0 €/mês, página no diretório, 1 pedido por mês.
  - **Profissional:** 49 €/mês + IVA, até 15 pedidos por mês no distrito, destaque, selo de verificado, alertas por SMS e email.
  - **Por pedido:** 12–25 € por contacto, sem mensalidade, cada pedido vendido a no máximo 3 empresas.

---

## 3. O que o site tem

1. **Cabeçalho fixo:** logótipo, menu (Como funciona, Preços, Sou profissional, Perguntas) e botão "Simular grátis".
2. **Topo:** título "Quanto custa remodelar a sua casa?", dois botões, três números (12 tipos de obra, 8 regiões, 0 €) e a planta de um T2 de 80 m² desenhada em SVG, com a etiqueta do preço de remodelar a cozinha e a casa de banho.
3. **Simulador em 5 passos**, com o resultado sempre visível ao lado:
   1. Tipo de imóvel: apartamento, moradia, escritório ou loja.
   2. Área (20–400 m²), quartos e salas, casas de banho, cozinhas, janelas, região e idade do edifício.
   3. Obras a fazer, com atalhos: Remodelação total, Só cozinha, Só casa de banho, Pintura e chão, Eficiência energética.
   4. Acabamentos: económico, médio ou premium.
   5. Extras e IVA: projeto e licenciamento, gestão de obra, imprevistos; IVA a 23%, 6% ou sem IVA.
4. **Resultado:** intervalo de preço animado, barra colorida com o peso de cada obra, custo por m², duração, valor médio, lista detalhada, totais com e sem IVA e comparação entre os três níveis de acabamento.
5. **Formulário de orçamentos:** nome, código postal, email, telemóvel, prazo e consentimento RGPD. Valida os dados, mas **ainda não envia para lado nenhum** (ver Pendentes).
6. **Como funciona:** Simule, Ajuste, Receba propostas.
7. **Exemplos de obras:** T2 em Lisboa (remodelação total), moradia no Centro (eficiência energética), escritório no Porto (pintura e chão). São calculados pelo simulador e abrem nele com um clique.
8. **Tabela de preços de referência** (boa para o Google).
9. **Secção para profissionais** com os três planos.
10. **Perguntas frequentes:** fiabilidade, custo de um T2, licenças, IVA a 6%, custo do serviço.
11. **Apelo final** em ocre e **rodapé** com 4 colunas.

---

## 4. Como o simulador calcula

Todos os preços estão em `index.html`, na tabela `WORKS` do script. São valores **sem IVA**, com mão de obra e materiais. Foram estimados por mim e **não estão validados** com empreiteiros.

| Trabalho | Quantidade usada | Económico | Médio | Premium |
|---|---|---|---|---|
| Demolições e entulho | área | 12 €/m² | 15 €/m² | 18 €/m² |
| Pavimentos | área | 25 €/m² | 45 €/m² | 90 €/m² |
| Pintura | área útil | 10 €/m² | 15 €/m² | 24 €/m² |
| Tetos falsos e pladur | 60% da área | 18 €/m² | 28 €/m² | 42 €/m² |
| Instalação elétrica | área | 35 €/m² | 50 €/m² | 75 €/m² |
| Canalização | área | 22 €/m² | 35 €/m² | 55 €/m² |
| Cozinha | nº de cozinhas | 6 000 € | 12 000 € | 25 000 € |
| Casas de banho | nº de casas de banho | 4 000 € | 7 500 € | 15 000 € |
| Janelas e caixilharia | nº de janelas (por defeito, área ÷ 12) | 450 € | 750 € | 1 300 € |
| Portas interiores | divisões + casas de banho + cozinhas | 220 € | 420 € | 850 € |
| Climatização | área | 40 €/m² | 70 €/m² | 120 €/m² |
| Isolamento térmico | área | 25 €/m² | 45 €/m² | 75 €/m² |

**Multiplicadores** (aplicados a todos os trabalhos):

- **Região:** Lisboa e Vale do Tejo ×1,15 · Grande Porto ×1,08 · Algarve ×1,10 · Norte (restante) ×0,93 · Centro ×0,95 · Alentejo ×0,93 · Madeira ×1,12 · Açores ×1,12
- **Idade do edifício:** menos de 20 anos ×1,00 · 20 a 50 anos ×1,08 · mais de 50 anos ×1,18
- **Tipo de imóvel:** apartamento ×1,00 · moradia ×1,06 · escritório ×0,95 · loja ×1,02

**Fórmula:**

1. Obra = soma de (quantidade × preço do nível × região × idade × tipo).
2. Extras sobre o valor da obra: projeto e licenciamento +6%, gestão de obra +5%, imprevistos +10% (ligado por defeito).
3. Total = (obra + extras) × (1 + IVA).
4. Intervalo mostrado: de 88% a 115% do total, arredondado a 500 €.
5. Duração em semanas = soma dos tempos de cada obra × 0,6, mais 6 semanas se houver projeto (mínimo 1 semana).

---

## 5. Identidade visual

**Cores (grafite e ocre).** O azul inicial foi trocado a pedido.

| Uso | Modo claro | Modo escuro |
|---|---|---|
| Fundo da página | `#f5f4f1` | `#121315` |
| Cartões | `#ffffff` | `#1b1d20` |
| Texto | `#1c1e21` | `#ecebe7` |
| Grafite (topo, cartão do resultado) | `#2b2f34` / `#17191c` | `#2b2f34` / `#0f1012` |
| Ocre (botões, destaques) | `#eaa21a` / `#f6c45a` | `#f0b13a` / `#f6c96a` |
| Texto de destaque | `#8a5a00` | `#f0b13a` |

No CSS, os nomes destas cores são `--escuro`, `--escuro-2`, `--ocre`, `--ocre-2`, `--realce` e `--realce-soft`.

**Letras (Google Fonts):**
- Títulos: Bricolage Grotesque
- Texto: Figtree
- Números: JetBrains Mono

**Elementos visuais:**
- padrão de azulejo português por trás das secções escuras;
- planta de arquitetura de um T2 no topo;
- a fotografia de obra fixa como fundo de **todo** o site, com as secções semitransparentes por cima.

**Logótipo escolhido: opção A, "Casa com euro", em grafite e ocre.** É o símbolo de uma casa com o € no lugar da porta, seguido de "QuantoCusta**Remodelar**" (com "Remodelar" em ocre).

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="64" height="64" viewBox="0 0 64 64">
  <path d="M7 31L32 10l25 21" fill="none" stroke="#22252a" stroke-width="6" stroke-linecap="round" stroke-linejoin="round"/>
  <path d="M14 27v27h36V27" fill="none" stroke="#22252a" stroke-width="6" stroke-linejoin="round"/>
  <path d="M41.5 35.2a8 8 0 1 0 0 11.6" fill="none" stroke="#eaa21a" stroke-width="4.5" stroke-linecap="round"/>
  <path d="M26 39h11M26 43.5h11" stroke="#eaa21a" stroke-width="3.5" stroke-linecap="round"/>
</svg>
```

Outras propostas estudadas, que estão em `docs/estudo-logotipos.html`: B etiqueta de preço com "?", C azulejo com casa, D rolo de pintura em "?", E fita métrica e F planta em forma de "Q". As paletas alternativas testadas foram verde-garrafa e mostarda, cimento e laranja, e castanho e areia.

---

## 6. Cronologia

1. Primeira versão do simulador, com o modelo de negócio, a tabela de preços e as perguntas frequentes.
2. Visual mais trabalhado: azulejo, planta no topo, ícones, botões + / −, exemplos de obras e comparação de acabamentos.
3. Fotografia de obra enviada pelo utilizador: primeiro como fundo do simulador, depois como fundo de todo o site.
4. Correção de um retângulo branco que aparecia no telemóvel. O texto de introdução partilhava um estilo com o painel de orçamentos.
5. Cores trocadas de azul cobalto para grafite e ocre.
6. Estudo de 6 logótipos. Escolhida a opção A, aplicada no cabeçalho, no rodapé e no ícone do separador.
7. Projeto separado do MM Detalhe:
   - criado o repositório próprio `QuantoCustaRemodelar`;
   - apagado o ramo provisório `quantocustaremodelar` do repositório MM-Detalhe-Automovel;
   - o `main` e o site do MM Detalhe nunca foram alterados.
8. Página 404 adicionada e GitHub Pages ativo.

---

## 7. Pendentes

- [ ] **Ligar o formulário de orçamentos** a um serviço (Formspree, Supabase, Google Sheets ou um CRM). No código, procure o comentário `Ligar aqui ao backend` em `index.html`.
- [ ] **Validar os preços** da tabela `WORKS` com empreiteiros reais.
- [ ] **Fotografia de fundo maior** (1920 px ou mais). A atual tem 770 px e fica desfocada em ecrãs grandes. Basta substituir `assets/obra-fundo.jpg` pelo mesmo nome.
- [ ] **Afinar o logótipo** e exportar as versões finais (PNG, versão para redes sociais e versão a preto).
- [ ] **Verificar a marca no INPI** antes de a usar comercialmente.
- [ ] **Domínio próprio** (por exemplo quantocustaremodelar.pt): verificar se está disponível, comprar e configurar no GitHub Pages.
- [ ] **Páginas legais:** Política de Privacidade, Termos e Livro de Reclamações. Os links do rodapé ainda não levam a lado nenhum.
- [ ] **Área de profissionais:** registo, pagamentos e distribuição dos pedidos. Hoje é só uma secção informativa.
- [ ] Opcional: ler o repositório `Quantocustacasar` para alinhar o modelo de negócio. Ainda não foi analisado.

---

## 8. Como recuperar na conta Claude Teams

1. **Garanta acesso ao repositório.** Na conta Teams, ligue o GitHub (claude.ai → Settings → Connectors) e instale a app Claude no repositório `bernas77764-glitch/QuantoCustaRemodelar`: https://github.com/apps/claude/installations/select_target. Se o repositório passar para uma organização da empresa, use a opção **Transfer** nas Settings do GitHub. O histórico vem junto.
2. **Abra uma sessão do Claude Code** com esse repositório selecionado.
3. **Cole este pedido para retomar:**

   > Este repositório é o site QuantoCustaRemodelar. Lê o `PROJETO.md` para teres o contexto completo (conceito, cálculo, identidade visual, logótipo escolhido e pendentes). Quero continuar a partir dos pendentes da secção 7.

4. As pré-visualizações no Claude (artifacts) da conta pessoal podem não passar para a conta Teams. Não faz mal: tudo o que lá estava está no repositório. Para ver o estudo de logótipos, abra `docs/estudo-logotipos.html` num browser ou peça ao Claude para o publicar de novo.

### Cópia de segurança extra (opcional)

No GitHub, abra o repositório, clique em **Code → Download ZIP** e guarde o ficheiro no computador ou no OneDrive ou Google Drive da empresa.
