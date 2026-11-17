# Vocabulary Games

Aplicativo para aprender vocabulário em inglês: veja a imagem, digite a palavra e escreva sua própria frase.
Tem 25 jogos, revisão espaçada, diário de escrita, progresso e tema claro/escuro. Roda no navegador e no Android.

O site é HTML/CSS/JS puro (sem framework). O [Capacitor](https://capacitorjs.com) o empacota como app Android,
e o GitHub Actions gera o APK automaticamente.

## Estrutura

```
www/index.html                 o aplicativo inteiro (edite aqui)
assets/                        ícones do app (1024x1024), usados para gerar os ícones do Android
capacitor.config.json          nome e ID do app (appId / appName)
package.json                   dependências e scripts
.github/workflows/android-apk.yml   gera o APK no GitHub
```

## Rodar no VS Code

1. Abra esta pasta no VS Code.
2. No terminal: `npm install`
3. `npm run dev` abre o site em http://localhost:5173
   (ou instale a extensão **Live Server** e abra `www/index.html`).

## Gerar o APK pelo GitHub (sem instalar nada)

1. Crie o repositório, faça commit e `git push` para a branch `main`.
2. Abra a aba **Actions** do repositório: o fluxo *Build Android APK* roda sozinho (leva uns 5 a 10 minutos).
3. Ao terminar, baixe o arquivo `vocabulary-games-apk` na seção **Artifacts** da execução.
4. Descompacte e instale `vocabulary-games.apk` no celular (ative "Instalar apps de fontes desconhecidas").

Para publicar na aba **Releases** com o APK anexado:

```bash
git tag v1.0.0
git push --tags
```

O APK gerado é de **debug** (instalável direto). Para publicar na Play Store é preciso um APK/AAB **assinado**
(release) com a sua chave; dá para adicionar depois com os *Secrets* do GitHub.

## Gerar o APK no seu computador (opcional)

Requisitos: Node 20, JDK 17 e Android Studio (ou o Android SDK).

```bash
npm install
npm run android:add     # só na primeira vez (cria a pasta android/)
npm run assets          # gera os ícones a partir de assets/
npm run sync            # copia www/ para o app
npm run android:open    # abre no Android Studio  (ou: npm run apk)
```

Depois de editar `www/index.html`, rode `npm run sync` de novo.

## Detalhes do Android

- **Voz em inglês:** o app usa a voz do celular. Se a pronúncia falhar em algum aparelho, instale o plugin nativo
  (o código já o usa automaticamente quando ele existe):
  `npm install @capacitor-community/text-to-speech` e rode `npm run sync`.
  Confira na página do plugin qual versão combina com o seu Capacitor.
- **Backup e diário:** no Android, "Exportar" abre a janela de compartilhar (salvar no Drive, enviar por WhatsApp etc.).
  Para restaurar, use "Importar" nos Ajustes e escolha o arquivo `.json`.
- **Seus dados** ficam salvos só no aparelho (armazenamento do app). Desinstalar apaga tudo, então faça backup.
- Mude nome e ID do app em `capacitor.config.json` (`appName`, `appId`) antes de publicar.

## Frases reais (Tatoeba)

O jogo *Frases reais* usa frases do [Tatoeba](https://tatoeba.org), licença
[CC BY 2.0 FR](https://creativecommons.org/licenses/by/2.0/fr/) (os créditos aparecem no app).
Baixe pares inglês–português em https://tatoeba.org/downloads e importe em **Ajustes → Frases reais**.
As frases são importadas por você; elas não vêm junto com o projeto.

## Observações

- As imagens das palavras são emojis do próprio aparelho, então o visual varia um pouco entre Android e navegador.
- O GitHub Actions não foi testado com o seu repositório: se algum passo falhar, abra a execução na aba Actions e
  me envie o erro que eu corrijo.
