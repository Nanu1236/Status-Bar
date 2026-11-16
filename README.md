# Estilo da Barra

App Android que desenha uma barra de estado personalizada por cima da original, com estilos prontos (Samsung One UI, Apple iOS, Xiaomi HyperOS), um editor completo e exportação para o Kustom (KLCK).

## O que faz

- **Estilos prontos**: One UI 6.1 a 9, iOS 15 a 27, MIUI 14 e HyperOS 1 a 3.1. São aproximações feitas à mão, não cópias exatas.
- **Editor**: posição e formato do relógio, estilo da bateria, sinal, Wi-Fi, velocidade da rede, operadora, tamanho, altura, margens, cantos e cores.
- **Mosaico nas definições rápidas** para ligar e desligar a barra num toque.
- **Exportar**: ficheiro `.klck` (experimental), receita com valores e fórmulas para o Kustom, e estilo em `.json` (exportar e importar).

## Limites (importante)

- Sem root, nenhuma app consegue trocar a barra de estado real do Android. Esta app desenha uma barra própria **por cima** da original, por isso o fundo tem de ser opaco para tapar a de baixo.
- Funciona através de um serviço de acessibilidade, só para ter permissão de desenhar a janela. A app não lê nem controla nada no ecrã.
- Em vídeos e jogos em ecrã inteiro no modo vertical a barra continua visível. Usa o mosaico das definições rápidas para a esconder. Em modo paisagem esconde-se sozinha (opção ligada por omissão).
- Sinal da rede: para ler as barras do operador e o 5G/4G a app precisa da permissão de telefone (botão "Permitir leitura do sinal da rede"). Sem ela, o sinal mostra-se sempre cheio.
- A exportação `.klck` usa um formato interno do Kustom que não é documentado oficialmente. Se o KLCK recusar o ficheiro, usa a receita.

## Compilar o APK só com o telemóvel (GitHub Actions)

1. Cria uma conta em github.com e um repositório novo (pode ser privado).
2. No repositório: **Add file > Create new file**. No nome escreve `.github/workflows/build.yml` (as barras criam as pastas) e cola o conteúdo do ficheiro `build.yml`. Grava com **Commit changes**.
3. **Add file > Upload files** e envia o `projeto.zip` (sem o descompactar). Grava com **Commit changes**.
4. Abre o separador **Actions**. O trabalho "Compilar APK" demora uns 3 a 6 minutos. Se não arrancar, escolhe-o e toca em **Run workflow**.
5. Quando acabar, vai a **Releases** (página principal do repositório) e descarrega `EstiloBarra.apk`.
6. Instala o APK (o Android pede para permitir instalar de fontes desconhecidas).

## Ativar no telemóvel

1. Abre a app **Estilo da Barra** e toca em **Abrir definições de Acessibilidade**.
2. Entra em **Aplicações instaladas** (ou "Serviços transferidos"), escolhe **Estilo da Barra** e ativa.
3. Se a opção aparecer cinzenta (Android 13 ou superior): **Definições > Aplicações > Estilo da Barra > menu ⋮ > Permitir definições restritas**, e volta ao passo 2.
4. Volta à app, escolhe um estilo e ajusta no editor.

## Importar no Kustom

Abre o KLCK, toca em importar e escolhe o ficheiro `estilo_barra.klck` que exportaste.

## Estrutura do código

- `StatusStyle.kt`: modelo do estilo, JSON e estilos prontos.
- `StatusBarView.kt`: desenho da barra (relógio, sinal, Wi-Fi, bateria) e leitura dos dados do sistema.
- `BarService.kt`: serviço de acessibilidade que mostra a barra por cima do sistema.
- `MainActivity.kt`: ecrã da app (pré-visualização, estilos, editor, exportar).
- `KlckExporter.kt`: gera o `.klck` e a receita.
- `ToggleTileService.kt`: mosaico das definições rápidas.
