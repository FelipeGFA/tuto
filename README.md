## 📋 1. Pré-requisitos (O que você precisa)

1.  **Computador (Windows)**.
2.  **Cabo USB** (para passar o arquivo para o celular).
3.  **Java (JDK)**: Necessário para gerar o aplicativo.
    *   *Baixe e instale:* [Eclipse Adoptium (JDK 17)](https://adoptium.net/pt-BR/download?link=https%3A%2F%2Fgithub.com%2Fadoptium%2Ftemurin17-binaries%2Freleases%2Fdownload%2Fjdk-17.0.17%252B10%2FOpenJDK17U-jdk_x64_windows_hotspot_17.0.17_10.msi&vendor=Adoptium).
    *   *Dica:* Na instalação, marque a opção "Set JAVA_HOME variable".
4.  **Git**: Ferramenta para baixar o código.
    *   *Baixe e instale:* [Git for Windows](https://git-scm.com/download/win). (Vá clicando em "Next").

---

## 📥 2. Baixando o Código Fonte

Vamos baixar apenas os arquivos necessários para economizar tempo.

1.  Crie uma pasta na sua Área de Trabalho chamada `Mihon-Ext`.
2.  Abra essa pasta, clique com o botão direito em um espaço vazio e selecione **"Open Git Bash here"**.
3.  Copie e cole os comandos abaixo na janela preta que abrir (um por um):

```bash
# 1. Clona o repositório base
git clone --filter=blob:none --sparse https://github.com/keiyoushi/extensions-source

# 2. Entra na pasta criada
cd extensions-source/

# 3. Configura o modo de download leve
git sparse-checkout set --cone --sparse-index

# 4. Adiciona as pastas de ferramentas
git sparse-checkout add buildSrc core gradle lib lib-multisrc utils

# 5. Adiciona a pasta da extensão MangaLivre
git sparse-checkout add src/pt/mangalivre
```

---

## ✏️ 3. Aplicando a Correção (Copiar e Colar Código)

Vamos atualizar os arquivos com a versão que funciona (créditos ao *rafaelbellintani*).

### 3.1 Substituir o `MangaLivre.kt`
1.  No computador, navegue até:
    `Mihon-Ext/extensions-source/src/pt/mangalivre/src/eu/kanade/tachiyomi/extension/pt/mangalivre/`
2.  Abra o arquivo `MangaLivre.kt` com o **Bloco de Notas**.
3.  Apague **tudo** o que está escrito nele.
4.  Copie o código deste link: [Novo código MangaLivre.kt](https://github.com/rafaelbellintani/extensions-source/blob/6387d053ff5df48036714623e804d35cb9df96b6/src/pt/mangalivre/src/eu/kanade/tachiyomi/extension/pt/mangalivre/MangaLivre.kt).
5.  Cole no Bloco de Notas e **Salve**.

### 3.2 Substituir o `build.gradle`
1.  Volte algumas pastas até: `Mihon-Ext/extensions-source/src/pt/mangalivre/`.
2.  Abra o arquivo `build.gradle` com o **Bloco de Notas**.
3.  Apague **tudo**.
4.  Copie o código deste link: [Novo código build.gradle](https://github.com/rafaelbellintani/extensions-source/blob/6387d053ff5df48036714623e804d35cb9df96b6/src/pt/mangalivre/build.gradle).
5.  Cole no Bloco de Notas e **Salve**.

---

## 🛠️ 4. Compilando a Extensão

Agora vamos criar o arquivo de instalação (`.apk`).

1.  Volte para o **Git Bash** (ou terminal). Certifique-se de estar dentro da pasta `extensions-source`.
2.  Execute o comando abaixo para iniciar a compilação (o ponto e a barra no início são importantes):

**Comando:**
```bash
./gradlew :src:pt:mangalivre:assembleDebug
```

*Nota: Isso pode demorar alguns minutos na primeira vez. Aguarde aparecer a mensagem **BUILD SUCCESSFUL**.*

---

## 📲 5. Instalando no Celular

O arquivo `.apk` foi criado no seu computador. Agora precisamos colocá-lo no celular.

### Localize o arquivo APK:
No seu computador, navegue até a pasta onde o arquivo foi gerado:
`extensions-source/src/pt/mangalivre/build/outputs/apk/debug/`
*(O arquivo deve se chamar `mangalivre-debug.apk` ou similar)*.

### Opção A: Instalação Manual (Mais Fácil)
1.  Conecte seu celular ao computador via cabo USB.
2.  No celular, se aparecer uma notificação, escolha a opção **"Transferência de Arquivos"** (MTP).
3.  No computador, copie o arquivo `mangalivre-debug.apk`.
4.  Abra o armazenamento do celular pelo computador e cole o arquivo em uma pasta fácil, como **Downloads**.
5.  **No Celular:** Abra seu gerenciador de arquivos, vá até a pasta Downloads e toque no arquivo `mangalivre-debug.apk`.
6.  Se o celular pedir permissão para instalar fontes desconhecidas, autorize e clique em **Instalar**.

### Opção B: Instalação via ADB (Avançado)
*Use esta opção apenas se você já tiver o ADB configurado e preferir usar linha de comando.*
1.  Certifique-se de ter o [Platform-tools](https://dl.google.com/android/repository/platform-tools-latest-windows.zip?hl=pt-br_) baixado e a Depuração USB ativada no celular.
2.  Abra o terminal na pasta do platform-tools.
3.  Digite: `adb install "caminho/do/seu/arquivo/mangalivre-debug.apk"`

---

## ⚙️ 6. Configuração Final no Mihon (Obrigatório)

Para carregar os capítulos, siga este passo a passo final:

1.  Abra o **Mihon**.
2.  Vá em **Navegar -> Extensões** e confira se "MangaLivre" está instalado (deve ter um ícone de aviso/escudo vermelho, pois não é oficial, clique em "Confiar").
3.  Tente abrir a obra MangaLivre na sua biblioteca.
4.  Clique no ícone do **Globo (WebView)** no topo direito da tela.
5.  No navegador que abrir, acesse um capítulo e espere as imagens carregarem. Se houver Captcha ("Sou humano"), resolva-o.
6.  Volte para o Mihon e arraste a tela para baixo para **Atualizar**.

Pronto! Os capítulos devem aparecer.
