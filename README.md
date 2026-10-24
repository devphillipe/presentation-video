# Presentation Video

Transforme o código de um site ou aplicativo em um **vídeo curto de lançamento** com o Codex e o [Hyperframes](https://www.npmjs.com/package/hyperframes).

> **Nome do repositório:** `presentation-video` · **Nome da skill no Codex:** `presentation-video` · **Comando:** `/presentation-video` (ou `$presentation-video`, conforme o cliente).

## O que a skill faz

A `/presentation-video` é uma *skill de orquestração*: ela lê o projeto local, define uma direção criativa inspirada em apresentações de produto, cria um roteiro e orienta o **Hyperframes**, responsável por implementar, validar e renderizar a composição. **Não** é um motor de vídeo independente nem exige uma URL pública do projeto.

- **Inspeção do projeto:** identifica proposta, interface, diferenciais, conteúdo e recursos visuais a partir do código.
- **Direção criativa e storyboard:** gera critérios visuais, cenas, textos, duração e transições específicos do produto.
- **Sete tons:** `default`, `polished`, `yc-parody`, `chaotic`, `deadpan`, `cinematic` e `app-store` — além de direções livres.
- **Formatos:** `landscape` (padrão), `vertical` e `square`.
- **Áudio:** orientação para trilha, efeitos sonoros e sincronização opcional com batidas; é possível desativá-los.
- **Renderização e revisão:** encaminha a composição ao Hyperframes, valida a saída, revisa o MP4 final e prepara o texto de divulgação.

O objetivo automático é um vídeo de **15–25 segundos**, mas `--duration` permite solicitar outra duração.

## Requisitos

- **Codex** com suporte a skills instaladas em `.codex/skills/`.
- **Node.js e npm/npx** para executar o Hyperframes.
- **Hyperframes** acessível ao ambiente do agente (CLI/instruções atualizadas). A skill depende dele para compor e renderizar.
- **Opcional para análise avançada de música:** Python **3.11+** com [`uv`](https://docs.astral.sh/uv/) e as dependências definidas em `scripts/pyproject.toml`. Sem essa etapa, o fluxo pode usar a análise de batidas suportada pelo Hyperframes ou seguir sem sincronização.
- Ferramentas e recursos extras podem ser exigidos pelo fluxo real de renderização configurado no Hyperframes.

## Instalação

### Windows (PowerShell)

```powershell
# Clone com o nome correto da skill (presentation-video)
git clone https://github.com/devphillipe/presentation-video.git "$env:USERPROFILE\.codex\skills\presentation-video"
```

### macOS / Linux

```bash
git clone https://github.com/devphillipe/presentation-video.git "${CODEX_HOME:-$HOME/.codex}/skills/presentation-video"
```

O diretório instalado deve se chamar `presentation-video` dentro de `skills/`, em conformidade com `name: presentation-video` no `SKILL.md`. Reinicie ou recarregue o Codex conforme necessário.

Verifique também se o Hyperframes está disponível no ambiente e se suas instruções podem ser lidas pelo agente. A execução efetiva dependerá dessa integração.

## Como usar

Abra no Codex o diretório do site ou aplicativo que será apresentado e solicite:

```text
/presentation-video
/presentation-video --tone polished --format vertical
/presentation-video --tone cinematic --duration 30 --title "Meu Aplicativo"
/presentation-video --tone chaotic --no-music --no-sfx
/presentation-video this. Make it feel like a ridiculous startup launch.
```

| Opção | Valores / efeito | Padrão |
| --- | --- | --- |
| `--tone` | `default`, `polished`, `yc-parody`, `chaotic`, `deadpan`, `cinematic`, `app-store` ou descrição livre | Inferido |
| `--format` | `landscape`, `vertical`, `square` | `landscape` |
| `--duration` | Duração do vídeo em segundos | Automática, 15–25 s |
| `--title` | Título personalizado | Inferido do projeto |
| `--no-music` | Não incluir música | Música habilitada |
| `--no-sfx` | Não incluir efeitos sonoros | SFX habilitados |

O agente deve respeitar a identidade do projeto, a legibilidade do texto, as instruções explícitas do usuário e a direção criativa acordada. Voz em off não é presumida: depende de solicitação específica.

## Etapas e entregáveis

1. **Inspecionar:** leitura do código e coleta das características do produto.
2. **Definir direção:** critérios visuais documentados em `apple-inspired-direction.md`.
3. **Planejar:** conceito e storyboard em `video-plan.md`.
4. **Compor:** `composition-brief.md` encaminhado ao Hyperframes e implementação em `composition/`.
5. **Validar e renderizar:** lint, pré-visualização, geração do MP4 e revisão em `video-qa.md`.
6. **Entregar:** vídeo `presentation-video.mp4` e sugestão de divulgação `share-copy.txt`.

Os resultados normalmente ficam na pasta `presentation-video-output/` do projeto, ou em `presentation-video-output-AAAA-MM-DD-HHMMSS/` para evitar sobrescrever execuções anteriores.

```text
presentation-video-output/
├── apple-inspired-direction.md
├── video-plan.md
├── composition-brief.md
├── composition/
├── presentation-video.mp4
├── video-qa.md
└── share-copy.txt
```

> A presença do arquivo final e a aprovação no QA dependem de uma execução bem-sucedida do Hyperframes. Quando houver bloqueios ou verificações incompletas, a skill deve informá-los em vez de afirmar sucesso.

## Estrutura do repositório

```text
presentation-video/
├── SKILL.md                  # Instruções principais da /presentation-video
├── agents/openai.yaml         # Metadados de exibição da skill
├── references/                # Inspeção, direção, planejamento, áudio e QA
├── scripts/                   # Análise opcional de cues musicais (Python)
├── assets/
│   ├── music/                 # Trilhas e metadados de batidas
│   └── sfx/                   # Biblioteca de efeitos e análise sonora
├── LICENSE
└── THIRD_PARTY_NOTICES.md
```

### Ferramenta opcional para metadados de música

```bash
cd scripts
uv sync
uv run python analyze_music_cues.py --help
```

Consulte [`references/audio.md`](references/audio.md) para escolher e sincronizar recursos de áudio.

## Licenças e créditos

O **código e a documentação próprios deste repositório** são disponibilizados sob a [Licença MIT](LICENSE), © 2026 Phillipe Oliveira.

Os **arquivos de música e efeitos sonoros de terceiros não passam a ser MIT**. As faixas “Happy Beats & Business Moves” são de **Sascha Ende / ENDE.APP**, sob **CC BY 4.0** e os SFX identificados nas referências são da **Kenney**, sob **CC0**. Consulte o arquivo [`THIRD_PARTY_NOTICES.md`](THIRD_PARTY_NOTICES.md) para os créditos e links oficiais. Respeite as condições aplicáveis também nos vídeos gerados.

## Contribuições

Issues e pull requests são bem-vindos. Ao alterar o fluxo, mantenha as referências e os exemplos sincronizados com `SKILL.md` e preserve os avisos de licença dos recursos de terceiros.
