## 📋 Pré-requisitos (O que você precisa)

Antes de começar, certifique-se de ter os itens abaixo:

1.  **Computador (Windows é o foco deste guia)**.
2.  **Cabo USB de Dados**: Não use apenas um cabo de carregar. O cabo precisa ser capaz de transferir arquivos entre o PC e o celular.
3.  **Celular Android** com o Mihon instalado.
4.  **Java (JDK)**: O computador precisa do Java instalado para compilar o código.
    *    Baixe e instale o [Eclipse Adoptium (JDK 17)](https://adoptium.net/pt-BR/download?link=https%3A%2F%2Fgithub.com%2Fadoptium%2Ftemurin17-binaries%2Freleases%2Fdownload%2Fjdk-17.0.17%252B10%2FOpenJDK17U-jdk_x64_windows_hotspot_17.0.17_10.msi&vendor=Adoptium). Durante a instalação, certifique-se de marcar a opção "Set JAVA_HOME variable".
5.  **Git**: Ferramenta para baixar o código.
    *   *Baixe aqui:* [Git for Windows](https://git-scm.com/download/win). Instale clicando em "Next" até o fim.

---

## 🚀 Passo 1: Preparando o Ambiente (ADB e Depuração USB)

Para instalar o aplicativo criado diretamente do computador para o celular, usaremos o **ADB**.

### 1.1 Baixar as Ferramentas de Plataforma
1.  Baixe o pacote oficial do Google: [Platform-tools (Windows)](https://dl.google.com/android/repository/platform-tools-latest-windows.zip?hl=pt-br_).
2.  Extraia o arquivo `.zip` para uma pasta de fácil acesso (exemplo: `C:\adb`).

### 1.2 Habilitar a Depuração USB no Celular
1.  Vá em **Configurações** > **Sobre o telefone**.
2.  Toque 7 vezes seguidas em **Número da versão** (ou "Número de compilação") até aparecer a mensagem "Você agora é um desenvolvedor".
3.  Volte, vá em **Sistema** > **Opções do Desenvolvedor**.
4.  Ative a opção **Depuração USB**.
5.  Conecte o celular ao PC com o cabo USB.
6.  Uma mensagem aparecerá na tela do celular perguntando se confia no computador. Marque "Sempre confiar" e toque em **Permitir**.

---

## 📥 Passo 2: Baixando o Código Fonte

Vamos baixar apenas os arquivos necessários do repositório oficial, para economizar tempo e internet.

1.  Abra a pasta onde você quer salvar o projeto (pode ser na Área de Trabalho).
2.  Clique com o botão direito em um espaço vazio e selecione **"Open Git Bash here"** (ou abra o Terminal/PowerShell e navegue até a pasta).
3.  Execute os comandos abaixo, um por um (copie e cole):

```bash
# 1. Clona o repositório base (sem baixar todos os arquivos ainda)
git clone --filter=blob:none --sparse https://github.com/keiyoushi/extensions-source

# 2. Entra na pasta criada
cd extensions-source/

# 3. Configura o modo de download esparso
git sparse-checkout set --cone --sparse-index

# 4. Adiciona as pastas essenciais do projeto
git sparse-checkout add buildSrc core gradle lib lib-multisrc utils

# 5. Adiciona APENAS a extensão do MangaLivre (o que nos interessa)
git sparse-checkout add src/pt/mangalivre
```

---

## ✏️ Passo 3: Atualizando o Código (A Correção)

O código oficial pode estar desatualizado. Vamos substituir dois arquivos com uma versão corrigida (créditos ao usuário *rafaelbellintani*).

### 3.1 Substituir o `MangaLivre.kt`
1.  No seu computador, navegue pelas pastas que você acabou de baixar até chegar em:
    `extensions-source/src/pt/mangalivre/src/eu/kanade/tachiyomi/extension/pt/mangalivre/`
2.  Você verá um arquivo chamado `MangaLivre.kt`.
3.  Abra este arquivo com o Bloco de Notas ou qualquer editor de texto.
4.  Apague **todo** o conteúdo dele.
5.  Acesse este link: [Código do MangaLivre.kt Corrigido](https://github.com/rafaelbellintani/extensions-source/blob/6387d053ff5df48036714623e804d35cb9df96b6/src/pt/mangalivre/src/eu/kanade/tachiyomi/extension/pt/mangalivre/MangaLivre.kt).
6.  Copie o código do site, cole no seu arquivo no Bloco de Notas e **Salvee**.

### 3.2 Substituir o `build.gradle`
1.  Volte algumas pastas até: `extensions-source/src/pt/mangalivre/`.
2.  Você verá um arquivo chamado `build.gradle`.
3.  Abra com o Bloco de Notas.
4.  Apague **todo** o conteúdo.
5.  Acesse este link: [Código do build.gradle Corrigido](https://github.com/rafaelbellintani/extensions-source/blob/6387d053ff5df48036714623e804d35cb9df96b6/src/pt/mangalivre/build.gradle).
6.  Copie o código do site, cole no seu arquivo e **Salve**.

---

## 🛠️ Passo 4: Compilando a Extensão

Agora vamos transformar esse código em um aplicativo instalável (`.apk`).

1.  Volte para o terminal (Git Bash ou PowerShell) dentro da pasta `extensions-source`.
2.  O repositório já possui uma ferramenta chamada `gradlew` que baixa tudo o que é necessário para compilar. Você não precisa instalar o Gradle manualmente, apenas o Java (Passo 1).
3.  Execute o comando de compilação:

**No Windows (PowerShell ou CMD):**
```powershell
.\gradlew :src:pt:mangalivre:assembleDebug
```

**No Linux/Mac ou Git Bash:**
```bash
./gradlew :src:pt:mangalivre:assembleDebug
```

*Nota: A primeira vez pode demorar alguns minutos pois ele baixará dependências da internet.*

Se tudo der certo, você verá a mensagem **BUILD SUCCESSFUL**.

---

## 📲 Passo 5: Instalando no Celular via ADB

Agora que o arquivo `.apk` foi criado, vamos instalá-lo no seu celular usando as ferramentas que baixamos no Passo 1.

1.  Certifique-se que o celular está conectado e desbloqueado.
2.  Localize onde você extraiu o **platform-tools** (ex: `C:\adb`).
3.  Copie o arquivo `.apk` gerado. Ele estará localizado na pasta do projeto em:
    `extensions-source/src/pt/mangalivre/build/outputs/apk/debug/`
    *(O arquivo deve se chamar algo como `mangalivre-debug.apk`)*.
4.  Cole esse arquivo APK dentro da pasta do `platform-tools` (junto com o `adb.exe`).
5.  Dentro da pasta `platform-tools`, segure **Shift**, clique com o botão direito em um espaço vazio e escolha **"Abrir janela do PowerShell aqui"** (ou Terminal).
6.  Execute o comando para instalar:

```powershell
.\adb install mangalivre-debug.apk
```

*Se aparecer "Success", a extensão foi instalada!*

---

## ⚙️ Passo 6: Configuração Final no Mihon

Para que a extensão funcione corretamente, é necessário um truque final devido às proteções do site.

1.  Abra o **Mihon** no celular.
2.  Vá em **Navegar** -> **Extensões** e verifique se o MangaLivre está lá e ativado.
3.  Vá na sua biblioteca ou na busca e tente abrir o MangaLivre.
4.  **Importante:** Clique no ícone do **Globo (WebView)** no canto superior direito para abrir o site dentro do app.
5.  Navegue pelo site, acesse um mangá e abra um capítulo qualquer. Se pedir Login ou resolver Captcha, faça isso.
6.  Após carregar as imagens no navegador, volte para o Mihon.
7.  Arraste a lista para baixo para **Atualizar**.

Agora os capítulos devem carregar normalmente pelo aplicativo
