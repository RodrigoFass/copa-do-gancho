# Copa do Gancho

Site do campeonato de Dead by Daylight entre amigos: de 6 a 10 jogadores, dois grupos, melhor de 3 nos grupos e melhor de 5 na grande final. Mostra a tabela de cada grupo, a partida da vez, bans, killers, mapas, ganchos e desempates.

Todo mundo com o link acompanha os placares. Só quem sabe a **senha de organizador** altera alguma coisa.

## Como funciona

- O site é um único arquivo, `index.html`, publicado pelo GitHub Pages.
- Os resultados ficam em `data.json`, na branch **`dados`** deste repositório. Cada salvamento vira um commit, então o histórico do campeonato fica registrado. Como os dados ficam fora da branch principal, salvar não faz o site ser publicado de novo.
- A senha protege uma chave do GitHub (fine-grained token) que só pode mexer neste repositório. A chave fica em `auth.json`, criptografada com a senha (PBKDF2 + AES-GCM). Quem digita a senha certa consegue salvar; o resto do público só lê.
- A página busca os resultados novos sozinha: a cada 20 s para organizadores e a cada 75 s para quem só está vendo.

## Colocando no ar

1. Crie um repositório **público** chamado `copa-do-gancho` e suba o `index.html` e este `README.md` na branch `main`.
2. Em **Settings → Pages**, escolha *Deploy from a branch*, branch `main`, pasta `/ (root)`.
3. Em um ou dois minutos o site fica em `https://SEU-USUARIO.github.io/copa-do-gancho/`.

## Criando a senha (uma vez só)

1. Crie uma chave em <https://github.com/settings/personal-access-tokens/new>:
   - **Repository access:** *Only select repositories* → `copa-do-gancho`.
   - **Permissions → Contents:** *Read and write*.
   - **Expiration:** uma data depois do fim do campeonato.
2. Abra o site, toque em **Entrar**, cole a chave e escolha a senha.
3. O site grava o `auth.json` e você já entra como organizador. Passe a senha para os outros organizadores.

Para trocar a senha: **Acesso → Trocar senha**. Quando o campeonato acabar, apague a chave em <https://github.com/settings/personal-access-tokens>. O site continua mostrando os resultados, só não dá mais para editar.

## Segurança, sem exagero

A senha serve para organizar quem mexe no campeonato. Ela não é um cofre: o `auth.json` é público, e uma senha fraca pode ser descoberta por tentativa. Mesmo assim, o máximo que alguém consegue com a chave é editar arquivos deste repositório. Use uma senha razoável e uma chave com validade curta.

## Outro nome de repositório

O site descobre usuário e repositório pelo endereço do GitHub Pages. Para testar fora dele, ajuste `owner` e `repo` no início do bloco "GitHub storage" no `index.html`.
