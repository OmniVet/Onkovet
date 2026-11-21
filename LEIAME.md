# ONKOVET — versão Firebase + GitHub Pages (100% gratuita)

Arquivos desta pasta:
- `index.html` – o sistema inteiro
- `firebase-config.js` – onde você cola os dados do seu Firebase e o e-mail master
- `firestore.rules` – regras de segurança do banco (quem lê, quem escreve, quem apaga)
- `.nojekyll` – arquivo vazio exigido pelo GitHub Pages

## Como funciona o acesso
- Todos entram com a **conta Google**.
- **Master** (você): vê tudo, exporta histórico (PDF/Word), apaga pacientes, edita protocolos, apresentações e doses, gerencia a equipe.
- **Equipe**: e-mails que você cadastra em *⚙ Admin → Equipe*. Cadastram e editam pacientes, sessões, terapias e solicitações de exame. Não apagam registros e não alteram as bibliotecas.
- Quem não está na lista vê "sem acesso" e nenhum dado.

## Passo a passo (cerca de 20 minutos)

### 1. Criar o projeto no Firebase
1. Acesse https://console.firebase.google.com e entre com sua conta Google.
2. **Adicionar projeto** → nome (ex.: `onkovet`) → pode desativar o Google Analytics → **Criar**.
3. Fique no plano **Spark** (gratuito). Não é preciso cartão.

### 2. Criar o banco (Firestore)
1. Menu **Criação → Firestore Database → Criar banco de dados**.
2. Local: `southamerica-east1` (São Paulo). Modo: **produção**.

### 3. Ligar o login Google
1. Menu **Criação → Authentication → Vamos começar**.
2. **Google** → Ativar → escolha o e-mail de suporte → Salvar.

### 4. Pegar os dados do app web
1. Engrenagem → **Configurações do projeto → Seus apps → ícone `</>` (Web)**.
2. Apelido `onkovet` → **Registrar app**.
3. Copie o bloco `firebaseConfig` e cole em `firebase-config.js` (substitua os valores `COLE_AQUI`).
4. Em `MASTER_EMAILS`, coloque o seu e-mail Google.

### 5. Colocar as regras de segurança
1. Firestore → aba **Regras**.
2. Apague tudo, cole o conteúdo de `firestore.rules`.
3. Troque `seu_email_master@gmail.com` pelo seu e-mail, **em letras minúsculas**.
4. **Publicar**.

### 6. Publicar no GitHub Pages
1. Crie uma conta em https://github.com e um repositório novo, **público** (ex.: `onkovet`). Repositório privado só publica páginas em plano pago.
   Os arquivos não contêm dados de pacientes: os dados ficam no Firebase, protegidos por login e regras.
2. **Add file → Upload files**: envie `index.html`, `firebase-config.js`, `firestore.rules`, `.nojekyll` (e este LEIAME, se quiser) → Commit.
3. **Settings → Pages → Source: Deploy from a branch → `main` / `(root)` → Save**.
4. Em 1–2 minutos o endereço aparece: `https://SEU-USUARIO.github.io/onkovet/`.

### 7. Autorizar o endereço no login
Firebase → Authentication → **Configurações → Domínios autorizados → Adicionar domínio** → `SEU-USUARIO.github.io`.

### 8. Primeiro acesso
1. Abra o endereço, **Entrar com Google** (com o e-mail master).
2. **⚙ Admin → Equipe**: adicione o e-mail Google de cada pessoa da equipe.
3. Em **Apresentações**, clique em *Importar lista do mercado*. Em **Protocolos**, *Importar modelos comuns*.
4. No celular/tablet: abra o endereço no navegador → menu → **Adicionar à tela inicial**.

### 9. Levar os dados da versão de teste (opcional)
Na versão antiga: **⚙ Admin → Exportar backup** (gera um arquivo .json).
Na nova, como master: **⚙ Admin → Importar backup** e escolha o arquivo.

## Limites do plano gratuito (Spark)
Valores aproximados na data desta versão — confira em firebase.google.com/pricing:
1 GiB de armazenamento, 50 mil leituras e 20 mil escritas por dia. Para um consultório isso é suficiente.
O GitHub Pages é gratuito para repositórios públicos.

## Avisos
- A restrição "só o master exporta" vale na tela. Quem tem acesso à equipe consegue ler os dados do banco (é inevitável em qualquer sistema desse tipo); por isso só cadastre pessoas de confiança. Já **apagar** é bloqueado pelas regras do banco para quem não é master.
- Esta versão foi montada e testada sem acesso ao Firebase real (a conexão é simulada nos testes). No primeiro uso, faça um cadastro de teste e confira se aparece em outro aparelho.
- Se aparecer "Missing or insufficient permissions", as regras não foram publicadas ou o e-mail das regras está diferente do e-mail da conta.
- Faça backup (⚙ Admin → Exportar backup) de tempos em tempos.
