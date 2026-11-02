# Roteiro das Aulas (app instalável)

Página única que funciona como aplicativo no celular: abre em tela cheia, funciona sem internet e guarda as aulas no próprio aparelho. Não precisa de loja de aplicativos.

## Publicar (uma vez só, no GitHub Pages)

1. Entre em github.com e crie um repositório **público** chamado `roteiro-aulas`. (Só o código do app fica lá. As aulas ficam no celular de cada professor, nunca no GitHub.)
2. No PowerShell, dentro desta pasta:

```
git init
git add .
git commit -m "Roteiro das Aulas"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/roteiro-aulas.git
git push -u origin main
```

3. No repositório: **Settings > Pages > Build and deployment > Source: Deploy from a branch > Branch: main, pasta / (root) > Save**.
4. Em cerca de 1 minuto o app fica em `https://SEU-USUARIO.github.io/roteiro-aulas/`. Esse é o link que você manda para os professores.

## Instalar no celular

- **iPhone:** abrir o link no **Safari**, tocar em Compartilhar (quadrado com seta) e em **Adicionar à Tela de Início**.
- **Android:** abrir no **Chrome**, tocar nos três pontos e em **Instalar app** (ou **Adicionar à tela inicial**).

Importante no iPhone: instalar na tela inicial protege as aulas contra limpeza automática do Safari.

## Trocar aulas entre professores

Em cada aula, o botão **Exportar** gera um texto (ou arquivo) para mandar por WhatsApp. Quem recebe toca em **Importar aula** e cola o texto ou escolhe o arquivo. Também serve como cópia de segurança.

## Publicar uma atualização

1. Troque os arquivos na pasta.
2. Em `sw.js`, aumente o número em `roteiro-aulas-v1` (para `v2`, `v3`...). Sem isso, quem já instalou pode continuar vendo a versão antiga.
3. `git add .`, `git commit -m "Atualização"`, `git push`.

## Arquivos

- `index.html`: o app inteiro
- `manifest.webmanifest`: nome e ícone do app instalado
- `sw.js`: faz funcionar sem internet
- `icons/`: ícones
