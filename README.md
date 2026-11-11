# 🎮 Retro Arcade - Emulador NES & SNES (HTML5 / EmulatorJS)

Uma aplicação web moderna, responsiva e pronta para uso offline/nuvem, desenvolvida em HTML5, CSS3 e JavaScript. O projeto utiliza o motor **EmulatorJS (WebAssembly)** para executar ROMs dos consoles **NES (8-bit)** e **SNES (16-bit)** diretamente no navegador.

Foi projetado especialmente para funcionar com **Smart TVs** (Samsung Tizen, LG webOS, Android TV), **computadores** e **dispositivos móveis**, com suporte completo a navegação por controle remoto, gamepads USB/Bluetooth e teclado.

---

## 🌟 Principais Recursos

- **Navegação Adaptada para Smart TVs**: Menu acessível com foco otimizado para controle remoto da TV e direcionais D-Pad.
- **Carregamento Flexível de ROMs**:
  - **Arquivo Local**: Carregamento instantâneo de uma ROM individual (`.nes`, `.smc`, `.sfc`, `.zip`).
  - **Pasta Local**: Varredura de uma pasta inteira no computador com detecção automática dos jogos disponíveis.
  - **Link / URL Direta**: Execução a partir de um link direto da web (ex: Dropbox com `dl=1` ou servidor próprio).
  - **Servidor HTTP Local (Modo TV)**: Varredura remota de pastas via servidor HTTP local com suporte a CORS.
- **Detecção Automática de Console**: Identifica o sistema correto (NES ou SNES) com base na extensão da ROM.
- **Suporte a Controles (Gamepads)**: Reconhecimento automático de controles USB e Bluetooth via Gamepad API, com menu de remapeamento manual.
- **Interface Estilo Streaming**: Design escuro e responsivo no estilo arcade/streaming.
- **Botão de Retorno Fácil**: Permite alternar de jogo ou voltar ao menu sem dar refresh manual.

---

## 📁 Estrutura do Repositório

```text
meu-repositorio/
├── index.html        # Código fonte da interface principal
├── README.md         # Documentação e guia do projeto
└── data/             # Arquivos e núcleos do EmulatorJS
    ├── loader.js
    ├── emulator.js
    ├── cores/        # Núcleos de emulação (nes_libretro, snes9x, etc.)
    └── localization/ # Idiomas da interface do emulador
```

> **Importante:** Para rodar de forma 100% offline, baixe o pacote de dados (`data/`) na aba de Releases oficiais do EmulatorJS no GitHub e extraia na raiz do projeto.

---

## 🚀 Como Executar

### 1. Executando Localmente (PC / Notebook)
Devido a restrições de segurança do navegador para scripts WebAssembly (`.wasm`), o projeto deve ser executado através de um servidor HTTP local.

- **Via VS Code**: Instale a extensão **Live Server** e clique em *Go Live*.
- **Via Python**: Abra o terminal na pasta do projeto e execute `python -m http.server 8000`.

---

### 2. Publicando no GitHub Pages (Para Smart TV e Acesso Remoto)

1. Faça o commit e push dos arquivos `index.html` e da pasta `data/` para o seu repositório no GitHub.
2. No GitHub, acesse **Settings** > **Pages**.
3. Em **Build and deployment > Branch**, selecione `main` (ou `master`) e `/ (root)`.
4. Clique em **Save**.
5. Em poucos minutos, sua página estará online no link fornecido pelo GitHub Pages.

---

## 📡 Servidor Local de ROMs com Suporte a CORS (para Smart TVs)

Se você hospedar o site no GitHub Pages e quiser que a sua Smart TV acesse as ROMs armazenadas no seu computador via Wi-Fi doméstica, crie um arquivo `server.py` na pasta onde guarda suas ROMs no PC:

```python
from http.server import HTTPServer, SimpleHTTPRequestHandler

class CORSRequestHandler(SimpleHTTPRequestHandler):
    def end_headers(self):
        self.send_header('Access-Control-Allow-Origin', '*')
        super().end_headers()

print("Servidor de ROMs rodando na porta 8000 com CORS ativado...")
HTTPServer(('0.0.0.0', 8000), CORSRequestHandler).serve_forever()
```

1. Execute no terminal: `python server.py`.
2. Na Smart TV, abra a página do GitHub Pages, digite o IP local do seu computador no campo de URL e clique em **Carregar da URL / Conectar Servidor**.

---

## ⚠️ Observação Legal

Este projeto é exclusivamente uma ferramenta de emulação de código aberto para fins educacionais e de preservação digital. Nenhuma ROM ou material protegido por direitos autorais é hospedado ou distribuído neste repositório.
