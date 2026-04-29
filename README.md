# Cerataúa – A Arte na Sua Mesa

Site de e-commerce estático para a Cerataúa, marca de cerâmicas artesanais brasileiras. Desenvolvido em HTML, CSS e JavaScript puro, sem dependências externas — funciona abrindo o `index1.html` diretamente no navegador.

---

## Estrutura do projeto

```
index1.html   # Arquivo único com todo o HTML, CSS e JS
README.md
```

Todo o código está concentrado em um único arquivo HTML auto-contido.

---

## Funcionalidades

### Navegação por páginas (SPA)
O site simula um roteamento de página única via JavaScript. As páginas disponíveis são:

| ID | Descrição |
|----|-----------|
| `home` | Página inicial com hero, destaques e promoções |
| `catalogo` | Catálogo completo com filtro por categoria |
| `search` | Resultados de busca |
| `historia` | Página "Nossa História" |
| `contato` | Formulário de contato |
| `carrinho` | Carrinho de compras |
| `checkout` | Formulário de finalização de pedido |
| `success` | Confirmação de pedido |

### Catálogo de produtos
Filtro por categoria em tempo real. Produtos atuais:

| Nome | Categoria | Preço |
|------|-----------|-------|
| Prato Guaraná | Pratos | R$ 46,90 |
| Prato Arara | Pratos | R$ 46,90 |
| Prato Capoeira | Pratos | R$ 46,90 |
| Caneca Brasil | Canecas | R$ 35,50 |

### Combos
| Nome | Itens | Preço |
|------|-------|-------|
| Kit Mesa Completa | Prato Guaraná + Prato Arara + Prato Capoeira + Caneca Brasil | R$ 149,90 |
| Dupla Pratos | Prato Guaraná + Prato Arara | R$ 79,90 |
| Capoeira & Café | Prato Capoeira + Caneca Brasil | R$ 69,90 |

### Carrinho
- Adicionar, remover e ajustar quantidade de itens
- Persistência via `localStorage` (chave: `cerataua_cart`)
- Cálculo automático de subtotal, frete e total
- Frete grátis para pedidos acima de R$ 150,00

### Cupons de desconto
| Código | Desconto |
|--------|----------|
| `ARTE10` | 10% |
| `CERATAUA20` | 20% |
| `PRIMEIRAPEDIDO` | 15% |

### Checkout
Formulário com campos de entrega (nome, CPF, e-mail, telefone, CEP, endereço) e seleção de forma de pagamento:
- Cartão de crédito (até 12x)
- Cartão de débito
- Pix (10% de desconto)
- Boleto bancário (vence em 3 dias úteis)

### Busca
Campo de busca com overlay de resultados em tempo real, filtrando por nome, categoria e descrição do produto.

### Modal de produto
Clique em qualquer card para abrir um modal com imagem ampliada, descrição completa e botão de adicionar ao carrinho.

---

## Tecnologias

- **HTML5** — estrutura e conteúdo
- **CSS3** — estilização completa inline no `<style>` (variáveis CSS, grid, flexbox, animações)
- **JavaScript (ES6+)** — lógica da aplicação inline no `<script>`
- **Google Fonts** — `Fredoka One` (títulos) e `Nunito` (corpo)
- **localStorage** — persistência do carrinho entre sessões

Nenhuma biblioteca ou framework externo é utilizado.

---

## Como usar

1. Abra o arquivo `index1.html` em qualquer navegador moderno.
2. Não é necessário servidor web — funciona via `file://`.

Para publicar, basta fazer o upload do `index1.html` em qualquer hospedagem estática (GitHub Pages, Netlify, Vercel, etc.).

---

## Adicionar produtos

Os produtos estão definidos no array `PRODUCTS` dentro do `<script>`:

```js
const PRODUCTS = [
  {
    id: 5,                        // ID único
    name: 'Nome do Produto',
    category: 'Categoria',        // usado no filtro
    price: 49.90,
    oldPrice: 59.90,              // null se não houver preço riscado
    emoji: 'Fallback',            // texto exibido caso não haja imagem
    img: 'URL ou base64',         // null se não houver imagem
    desc: 'Descrição do produto.',
    featured: true,               // aparece na seção de destaques
    badge: null,                  // ex: 'Novo' ou 'Promo'
  },
];
```

---

## Funções principais (JS)

| Função | Descrição |
|--------|-----------|
| `navigate(page)` | Troca a página visível |
| `addToCart(id, event)` | Adiciona produto ao carrinho |
| `removeFromCart(id)` | Remove produto do carrinho |
| `changeQty(id, delta)` | Altera quantidade de um item |
| `applyCoupon()` | Valida e aplica cupom de desconto |
| `renderCatalog()` | Renderiza o grid de produtos com filtro ativo |
| `renderCart()` | Renderiza os itens do carrinho |
| `renderCheckout()` | Renderiza o resumo e opções de pagamento |
| `placeOrder()` | Finaliza o pedido e limpa o carrinho |
| `runSearch(q)` | Executa busca e navega para a página de resultados |
| `openModal(id)` | Abre o modal de detalhe do produto |
| `toast(msg)` | Exibe uma notificação temporária |

---

## Personalização rápida

**Cores principais** — variáveis CSS no `:root`:
```css
--orange:    #F5A623;
--brown:     #3B1A06;
--cream:     #FFF8EC;
--green:     #2D6A4F;
```

**Cupons** — objeto `COUPONS` no script:
```js
const COUPONS = {
  'MEUCUPOM': 15,  // 15% de desconto
};
```

**Frete grátis** — threshold definido em `renderCartSummary` e `renderCheckout`:
```js
const frete = subtotal > 150 ? 0 : 15.90;
```
