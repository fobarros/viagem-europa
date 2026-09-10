# viagem-europa

Página única que abre um roteiro de viagem **cifrado**, para leitura no celular.

## O que está aqui

Só o `index.html`. Ele carrega o conteúdo já criptografado com **AES-256-GCM**,
com chave derivada da senha por **PBKDF2-SHA256, 600.000 iterações**. A
decifragem acontece no navegador, via WebCrypto, dentro do próprio aparelho.

**A senha não está neste repositório** e nunca é enviada a servidor nenhum —
não há back-end, não há formulário que poste nada. Quem não tiver a senha vê só
bytes embaralhados.

Como é uma página estática, **não existe bloqueio por tentativas**. A única
proteção é a força da senha.

## Como republicar depois de mudar o roteiro

O conteúdo em claro e o script que cifra ficam **fora deste repositório**, no
repo privado `fobarros/viagem-europa-hidden`. Aqui só entra o resultado.

```powershell
cd "C:\Dev\viagem-europa-hidden"
node tools\publicar.mjs
```

O script pede a senha na tela (sem eco), calcula sozinho a pasta irmã
`viagem-europa-web` e regrava o `index.html` lá — não depende de usuário nem
de drive fixo. Depois é só commitar **esse arquivo**:

```powershell
cd C:\Dev\viagem-europa-web
git add index.html
git commit -m "Atualiza roteiro"
git push
```

O GitHub Pages leva um ou dois minutos para publicar.

## Regra dura

**Nada em claro entra aqui.** Nem o HTML de origem, nem os markdown do projeto,
nem a pasta de reservas. O `.gitignore` já bloqueia tudo por padrão e libera só
`index.html`, `.gitignore` e `README.md` — não afrouxe.
