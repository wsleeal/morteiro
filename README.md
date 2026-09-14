# Calculadora de Balística

Calculadora de distância e azimute para coordenadas de jogo. Funciona no navegador, com HTML, CSS, JavaScript e Alpine.js. O servidor Python é opcional para uso local; o GitHub Pages não precisa executar Python.

## GitHub Pages

O workflow `.github/workflows/deploy-pages.yml` publica automaticamente a cada push na branch `master`. Também pode ser iniciado manualmente em **Actions → Deploy GitHub Pages → Run workflow**.

Configuração inicial:

1. No repositório `wsleeal/morteiro`, abra **Settings → Pages → Build and deployment → Source** e selecione **GitHub Actions**.
2. Envie os arquivos do projeto, incluindo `.github/workflows/deploy-pages.yml`, para a branch `master`.
3. Aguarde a conclusão do job `deploy` na aba **Actions**. A URL publicada aparece no ambiente `github-pages`.

Endereço esperado: [wsleeal.github.io/morteiro](https://wsleeal.github.io/morteiro/).

A pipeline copia somente `src/morteiro/index.html` e `src/morteiro/favicon.svg` para o artefato de publicação e adiciona `.nojekyll`. Edite esses arquivos diretamente: não é necessário manter outra cópia em `docs`, instalar dependências ou criar uma branch de publicação. O ícone usa caminho relativo para funcionar no subdiretório `/morteiro/`.

O deploy usa o `GITHUB_TOKEN` automático, sem token pessoal ou segredo adicional. O repositório precisa permitir GitHub Pages e GitHub Actions. Se a branch de publicação mudar, atualize `on.push.branches` no workflow e eventuais regras do ambiente `github-pages`.

Se o primeiro workflow falhar antes de configurar o Pages, execute-o novamente em **Actions** após selecionar a fonte **GitHub Actions**.

Referência: [workflows personalizados do GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages).

## Como usar

Informe a origem (`x101.33, y59.98`). Use **Adicionar destino** para abrir o modal, preencher um nome opcional e as coordenadas (`x97.27, y61.27`) e confirmar em **Adicionar**. As coordenadas são validadas antes de criar o cartão.

O lápis abre a edição do destino e a lixeira remove o cartão. Ao editar, os resultados anteriores desse destino são limpos. Para fechar o modal sem salvar, use **Cancelar**, Escape ou clique no fundo. Marque **Fixar origem** para bloquear sua edição.

Clique em **Calcular** para obter os resultados de todos os destinos:

- Distância em metros: `√((destino.x − origem.x)² + (destino.y − origem.y)²) × 100`. Para os exemplos acima, aproximadamente `426,00 metros`.
- Azimute em graus, no sentido horário a partir do norte, considerando X crescente para leste e Y crescente para norte. Para pontos iguais, o azimute é indefinido.

Aceita números negativos e espaços entre os componentes. Use ponto como separador decimal. Em celulares, os cartões e resultados se adaptam à largura disponível.

O Alpine.js 3.15.3 é carregado por CDN; é necessária conexão com a internet para carregar essa biblioteca e usar os modais.

## Execução local

Com `uv`, na pasta do projeto:

```powershell
uv run python -m morteiro
```

Ou instale com Python 3.14 ou superior:

```powershell
python -m pip install -e .
python -m morteiro
```

Abra http://127.0.0.1:8000. Para usar outra porta:

```powershell
python -m morteiro --port 8080
```

Encerre com Ctrl+C. Após instalar, também é possível iniciar com `morteiro`.
