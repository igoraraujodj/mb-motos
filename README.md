# MB Motos

Site em [`mb-motos/`](mb-motos/).

A pasta existe por um motivo prático: o projeto da Vercel foi criado com o
campo **Root Directory** apontando para `mb-motos`, e ele fica gravado nas
configurações do projeto. Enquanto esse campo estiver assim, a Vercel
procura o site dentro dessa pasta, e um repositório com o site na raiz faz
todo deploy falhar em um segundo, antes mesmo de começar a build.

Para achatar isso depois (site direto na raiz), é só limpar o campo Root
Directory em Settings, Build and Deployment, e mover os arquivos de volta.
