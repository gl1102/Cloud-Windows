[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Čeština](README.cs.md) | [Dansk](README.da.md) | [Deutsch](README.de.md) | [Esperanto](README.eo.md) | [فارسی](README.fa.md) | [Suomi](README.fi.md) | [Français](README.fr.md) | [Ελληνικά](README.gr.md) | [Magyar](README.hu.md) | [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [മലയാളം](README.ml.md) | [Nederlands](README.nl.md) | [Norsk](README.no.md) | [Polski](README.pl.md) | [Português](README.ptbr.md) | [Română](README.ro.md) | [Türkçe](README.tr.md) | [Українська](README.ua.md) | [Tiếng Việt](README.vn.md)

# ☁️ Cloud-Windows — Área de trabalho Windows gratuita na nuvem

Transforme uma VM Windows gratuita do GitHub Actions em uma área de trabalho na nuvem acessível pelo navegador. Abra uma página da web e você tem um PC com Windows — desligue quando terminar. Totalmente grátis.

## ✨ Recursos

- 🖥️ Uma área de trabalho Windows completa, direto no seu navegador (cliente web noVNC)
- 📐 **Resolução automática**: após abrir a página, a resolução da área de trabalho se ajusta automaticamente ao tamanho da janela do navegador — celulares e PCs ficam com o ajuste ideal; ela acompanha quando você redimensiona a janela também
- 🌐 Acesso via Cloudflare Tunnel — sem IP público, sem necessidade de NAT traversal
- ⌨️ IME Sogou Pinyin integrado, a entrada em chinês funciona de imediato (pressione `Win + Space` para alternar entre chinês e inglês)
- 🖱️ Conecte-se pelo celular, tablet ou computador
- ⏱️ Cada execução dura até ~6 horas, e você pode cancelar a qualquer momento
- 📦 **Edição RustDesk**: há também um workflow do RustDesk que baixa automaticamente a versão mais recente do RustDesk para o disco D e o instala silenciosamente em `D:\RustDesk`

## 🚀 Uso (funciona logo após fazer fork)

### Etapa 1: Faça um fork deste projeto

Clique no botão **Fork** no canto superior direito desta página para copiar o projeto para a sua conta do GitHub. Depois do fork, você estará no repositório `your-username/Cloud-Windows`.

> 💡 Por que fazer fork? O GitHub Actions só pode ser executado em repositórios da sua própria conta — o fork dá a você permissão para executá-lo.

### Etapa 2: Inicie a área de trabalho na nuvem

1. Acesse a página do seu repositório com fork e clique na aba **Actions** no topo
2. Escolha um workflow à esquerda (escolha um):
   - **Windows Cloud Desktop**: a área de trabalho na nuvem padrão
   - **Windows Cloud Desktop + RustDesk**: edição padrão mais download automático do RustDesk mais recente para o disco D com instalação silenciosa em `D:\RustDesk` (a versão não está fixa — sempre busca a última versão oficial)
3. Clique no botão **Run workflow** à direita — uma caixa de diálogo com três campos aparece:

| Parâmetro | Descrição |
|------|------|
| VNC password | A senha que você vai digitar ao se conectar à área de trabalho — apenas letras e números, até 8 caracteres (ex.: `abc12345`). **Anote-a** |
| Run duration | Por quantos minutos esta sessão da área de trabalho na nuvem ficará ativa. Padrão 300 (5 horas), máximo 350 |
| Resolution | A resolução inicial da área de trabalho, padrão 1920x1080; assim que você abrir a página no navegador, ela se ajusta automaticamente ao tamanho da janela |

4. Clique no botão verde **Run workflow** para confirmar — a área de trabalho na nuvem começa a inicializar

### Etapa 3: Obtenha o URL de acesso

1. Na página Actions, entre na execução que você acabou de iniciar (a de cima — um ponto amarelo significa que está rodando)
2. Aguarde cerca de 3–5 minutos para a VM instalar o software e configurar o túnel
3. Clique na etapa **启动服务并建立隧道**, expanda os logs e role para baixo para encontrar um URL como este:

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. Copie o URL e abra-o no seu navegador (o navegador nativo do celular funciona bem)

### Etapa 4: Conecte-se à área de trabalho

1. Na página do noVNC que abrir, clique em **Connect**
2. Digite a senha VNC que você definiu na Etapa 2
3. Você entrou — aproveite sua área de trabalho Windows 🎉
4. A resolução da área de trabalho se ajustará automaticamente à janela do navegador em cerca de 10 segundos após abrir a página; redimensionar a janela aciona um novo ajuste automático (escolhido entre as resoluções suportadas pela sua GPU)

> ⌨️ Pressione **Win + Space** para alternar o método de entrada entre Sogou Pinyin e o teclado em inglês.

### Etapa 5: Desligue quando terminar

- Volte para a página Actions, abra a execução e clique em **Cancel run** no canto superior direito — a VM é destruída e o túnel cai
- Ela também termina automaticamente quando o tempo definido acaba, então não se preocupe com ela rodando para sempre

## ⚠️ Observações

- **O URL muda a cada execução**: o URL antigo para de funcionar assim que a execução anterior termina, então use sempre o URL dos logs da execução mais recente
- **Nada é salvo**: quando a VM é destruída, arquivos, downloads e estados de login na área de trabalho são apagados — mova arquivos importantes a tempo
- **Regras de senha**: apenas letras e números, até 8 caracteres — senhas mais longas ou com caracteres especiais podem falhar ao conectar (com `Authentication failed`)
- **Não clique em Re-run**: para iniciar uma nova área de trabalho, clique em **Run workflow** — o Re-run repete o código antigo
- **Conexão lenta/travando**: o túnel passa pela Cloudflare; as velocidades da China continental dependem da sua rede, mas é utilizável
- **A página não abre**: primeiro verifique se a execução ainda está em andamento (ponto amarelo) — se foi cancelada ou concluída, o URL está morto

## ❓ FAQ

| Sintoma | Causa / Correção |
|------|-----------|
| `loopback connections are not enabled` | Bug de versão antiga — inicie uma nova execução com o código mais recente via Run workflow |
| `Server is not configured properly` | Bug de versão antiga — inicie uma nova execução com o código mais recente via Run workflow |
| `Authentication failed` | Senha VNC errada, ou a senha tem mais de 8 caracteres / contém caracteres especiais |
| 502 / 1033 na página | O túnel ainda não subiu ou caiu — aguarde alguns minutos ou execute novamente |
| A resolução não mudou automaticamente | Aguarde ~10 segundos; certifique-se de que a janela do navegador realmente mudou de tamanho; algumas resoluções não padrão não são suportadas pela GPU e a mais próxima é escolhida |

## 🛠️ Quer personalizar por conta própria?

Os arquivos de workflow ficam em `.github/workflows/` (`windows-vnc.yml` para a edição padrão, `windows-vnc-rustdesk.yml` para a edição RustDesk) — você pode editá-los direto no site do GitHub; as mudanças entram em vigor após o commit.
