# Origem e destino

Página local com dois campos para coordenadas, usando apenas a biblioteca padrão do Python.

Na pasta do projeto, execute:

```powershell
uv run python src/morteiro/server.py
```

Se `python` já estiver disponível no terminal, você pode executar `python src/morteiro/server.py` diretamente.

Abra http://127.0.0.1:8000 no navegador. Para usar outra porta:

```powershell
python src/morteiro/server.py --port 8080
```

Cole a origem (`x101.33, y59.98`) e o destino (`x97.27, y61.27`). A página valida e exibe os pontos e permite limpar os campos. Marque “Fixar origem” para bloquear sua edição; nesse caso, o botão de limpar apaga somente o destino. Aceita números negativos e espaços entre os componentes. Use ponto como separador decimal.

Clique em “Calcular distância” para obter a distância em metros: `√((destino.x − origem.x)² + (destino.y − origem.y)²) × 100`. O resultado é exibido com duas casas decimais. Para os exemplos acima, o resultado é aproximadamente `426,00 metros`.

O resultado também mostra o azimute em graus, no sentido horário a partir do norte, considerando X crescente para leste e Y crescente para norte. Para pontos iguais, o azimute é indefinido.

Encerre o servidor com Ctrl+C. Se o projeto estiver instalado, também é possível iniciar com `morteiro` ou `python -m morteiro`.
