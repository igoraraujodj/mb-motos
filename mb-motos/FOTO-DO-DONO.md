# Foto do dono no topo do site

Especificação do arquivo e prompts de geração. O encaixe já está pronto no
código: quando o arquivo existir, é só apontar em `config.js`.

---

## 1. O que o site precisa receber

| Arquivo | Uso | Medida | Formato |
|---|---|---|---|
| `dono.png` | Desktop, coluna do meio | **1200 x 1600 px** (3:4) | PNG com **fundo transparente** |
| `dono-mob.png` | Celular, plano de fundo do título | **900 x 1200 px** (3:4) | PNG com **fundo transparente** |

**Por que recorte transparente, e não foto com fundo:** o topo do site é
preto, e qualquer fundo, mesmo escuro, aparece como um retângulo mais claro
atrás dele. Com recorte, a base da imagem dissolve no preto da página por
uma máscara em degradê, e ele parece estar dentro da cena.

Regras do recorte:

- **Enquadramento**: dos joelhos para cima (desktop) e do peito para cima
  (celular). Corpo inteiro fica pequeno demais na coluna.
- **Corpo colado na base do arquivo**: nada de margem embaixo, porque a
  imagem é alinhada pelo pé do quadro.
- **Folga de 8% no topo** para a cabeça não encostar na borda.
- **Peso**: até 250 KB por arquivo. Exporte o PNG e passe no
  [squoosh.app](https://squoosh.app) se passar disso.
- **Cabelo recortado com cuidado**: é onde recorte automático costuma
  falhar, e num fundo preto o halo branco denuncia na hora.

---

## 2. Zona segura do texto

No desktop ele fica na **coluna do meio**: texto à esquerda, formulário à
direita. Ou seja, a área dele é uma faixa vertical central, e nada de texto
passa por cima. No celular ele vira plano de fundo à direita, com 30% de
opacidade, e aí o texto passa por cima mesmo, por isso a versão fechada
precisa ter o rosto no terço superior.

Pela regra dos grids: o rosto fica no terço superior do quadro, e o colchão
entre a borda da cabeça e a área de texto é de no mínimo 15% da largura.

---

## 3. Prompts de geração

Use as três fotos do rosto dele como referência facial no gerador (Nano
Banana, Flux com referência, Midjourney com `--cref`, Seedream). A pele, a
barba e o formato do rosto precisam vir das fotos, não da imaginação do
modelo.

### Opção A — Retrato de autoridade (a principal)

> Retrato fotográfico de homem brasileiro de 30 a 40 anos, pele morena
> clara, cabelo escuro curto, barba curta, sorriso leve e confiante, usando
> camisa polo preta com detalhes vermelhos e o logo MB Motos bordado no
> peito. Enquadramento dos joelhos para cima, câmera ligeiramente abaixo da
> linha dos olhos, olhando para a câmera com expressão de quem domina o que
> faz. Braços cruzados, ombros abertos. Iluminação de estúdio com luz
> principal vinda da esquerda e contraluz sutil marcando o contorno dos
> ombros, fundo preto sólido. Fotografia editorial, nitidez alta no rosto,
> proporção 3:4, corpo alinhado à base do quadro.

### Opção B — Ambiente de oficina (mais real, menos estúdio)

> Retrato fotográfico de homem brasileiro de 30 a 40 anos, pele morena
> clara, barba curta, camisa polo preta com detalhes vermelhos e logo MB
> Motos, de pé ao lado de uma moto sobre a rampa de uma oficina. Câmera
> abaixo da linha dos olhos, olhar direto para a câmera, expressão
> tranquila e confiante, mão apoiada no guidão. Luz de oficina com contraste
> alto, fundo escuro e desfocado, faíscas de luz quente ao fundo. Fotografia
> documental, proporção 3:4, dos joelhos para cima.

### Opção C — Silhueta recortada com contraluz (a mais gráfica)

> Retrato fotográfico de homem brasileiro de 30 a 40 anos, camisa polo preta
> com detalhes vermelhos, braços cruzados, enquadrado do peito para cima,
> câmera abaixo da linha dos olhos. Contraluz vermelha intensa marcando o
> contorno dos ombros e da cabeça, luz frontal fraca revelando o rosto,
> fundo preto absoluto. Estilo de cartaz esportivo, alto contraste,
> proporção 3:4.

**Depois de gerar**: remova o fundo (remove.bg, Photoroom ou a própria
ferramenta) e exporte em PNG transparente nas medidas da tabela acima.

---

## 4. Tratamento aplicado pelo site

O que já acontece por CSS, sem precisar vir na imagem:

- **Dissolução na base**: degradê que apaga os últimos 20% da imagem.
- **Assinatura**: nome e cargo ao pé da foto, com um traço amarelo.
- **Celular**: opacidade de 30%, para o texto continuar legível por cima.

Se quiser testar outro tratamento antes de decidir, os três abaixo são
trocas de uma linha no CSS:

| Tratamento | Efeito |
|---|---|
| Duotone vermelho | `filter: grayscale(1) sepia(1) hue-rotate(-25deg) saturate(4)` |
| Contorno de luz | `drop-shadow(0 0 24px rgba(227,6,19,.45))` |
| Preto e branco com o logo colorido | `filter: grayscale(1) contrast(1.1)` |
