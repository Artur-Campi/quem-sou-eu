# Quem sou eu? — site próprio

Um arquivo só (`index.html`). Sem npm, sem build, sem framework. Só precisa de um banco Firebase grátis e de um lugar para hospedar.

## 1. Criar o banco (5 minutos, grátis)

1. Entre em https://console.firebase.google.com e clique em **Criar um projeto**. Pode recusar o Google Analytics.
2. No menu lateral, em **Criação**, abra **Realtime Database** e clique em **Criar banco de dados**.
   - Região: `us-central1` serve bem para o Brasil.
   - Escolha **Iniciar no modo de teste**.
3. Ainda no console, clique na engrenagem > **Configurações do projeto** > role até **Seus apps** > ícone `</>` (Web) > registre o app.
4. Copie o objeto `firebaseConfig` que aparece.

Confira se o `firebaseConfig` tem o campo `databaseURL`. Se não tiver, o passo 2 não foi concluído.

## 2. Colar no arquivo

Abra o `index.html` num editor de texto. Logo no começo do `<script type="module">` existe um bloco assim:

```js
const FIREBASE_CONFIG = {
  apiKey: "",
  ...
};
```

Substitua pelo objeto que você copiou. Salve.

## 3. Regras do banco

O modo de teste expira em 30 dias. Para o jogo não parar de funcionar, vá em **Realtime Database > Regras** e use:

```json
{
  "rules": {
    "salas": {
      "$codigo": {
        ".read": true,
        ".write": true
      }
    }
  }
}
```

Isso deixa as salas abertas para quem souber o código de 4 letras. É um jogo de festa sem dado pessoal, então o risco é baixo. Se quiser fechar depois, dá para trocar por autenticação anônima.

## 4. Publicar

Qualquer hospedagem de site estático serve. Duas opções fáceis:

**GitHub Pages**
1. Crie um repositório público novo.
2. Suba o `index.html` na raiz.
3. Settings > Pages > Source: `Deploy from a branch`, branch `main`, pasta `/root`.
4. Em um ou dois minutos o link `https://seuusuario.github.io/nome-do-repo/` fica no ar.

**Netlify**
1. Entre em https://app.netlify.com/drop.
2. Arraste a pasta com o `index.html`.
3. O link sai na hora e dá para renomear em Site settings.

## Jogando

Mande o link para os três amigos, você cria a sala, eles entram com o código de 4 letras. Chamada de vídeo por fora, porque as perguntas são faladas.
