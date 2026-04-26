# Quiz Manu — Mobile & Score Fix

## Scope

Dois arquivos: `ciencias_1.html` (nível normal) e `ciencias_2.html` (nível expert).  
Mudanças idênticas de lógica JS e CSS nos dois arquivos.

---

## 1. Bug: Pontuação em questão errada

### Problema
Quando o usuário erra uma opção, o botão fica desabilitado mas as demais continuam disponíveis. Se o usuário achar a resposta correta na segunda ou terceira tentativa, `score++` é executado normalmente — o ponto é concedido mesmo com erro anterior.

### Solução
Adicionar flag `failed` no escopo do módulo.

- `render()` reseta `failed = false` a cada nova pergunta.
- `pick()` — branch errado: `failed = true`.
- `pick()` — branch correto: `score++` e atualização do display só executam se `!failed`.
- Animação de correto (verde), feedback e botão "próxima" aparecem normalmente — a usuária vê qual era a resposta certa, mas o placar não sobe.

---

## 2. Melhorias Mobile

### 2a. Tap highlight e seleção de texto
Nos botões (`.opt-btn`, `.start-btn`, `.next-btn`, `.restart-btn`):
```css
user-select: none;
-webkit-tap-highlight-color: transparent;
```
Evita flash cinza/azul ao tocar e seleção acidental de texto.

### 2b. Hover em touch
```css
@media (hover: none) {
  .opt-btn:hover:not(:disabled) {
    transform: none;
    /* mantém cor/borda */
  }
  .opt-btn:active:not(:disabled) {
    transform: scale(0.96);
  }
}
```
Remove o `translateX(4px) scale(1.01)` que em mobile fica "preso" após o toque. Substitui por `:active` com scale para feedback visual.

### 2c. Telas pequenas (≤ 400px)
Media query `@media (max-width: 400px)` reduz:

| Elemento | Antes | Depois |
|---|---|---|
| `.q-text` font-size | 20px / 19px | 16px |
| `.opt-btn` font-size | 18px / 17px | 15px |
| `.opt-btn` padding | 18px 22px | 14px 16px |
| `.logo` font-size | 26px | 20px |
| `.q-emoji-big` font-size | 72px | 52px |
| `.start-title` font-size | 32px | 26px |
| `.start-btn` / `.next-btn` font-size | 22–24px | 18–20px |
| `.q-card` padding | 28px 24px 24px | 20px 16px 18px |
| `.wrapper` padding top | 24px | 14px |

---

## Arquivos a modificar

- `ciencias_1.html` — JS (`pick`, `render`) + CSS (3 blocos)
- `ciencias_2.html` — JS (`pick`, `render`) + CSS (3 blocos)

Sem novos arquivos. Sem dependências externas.
