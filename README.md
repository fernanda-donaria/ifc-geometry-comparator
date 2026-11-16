# ifc-geometry-comparator

Ferramenta de análise de divergências geométricas entre capturas de visualizadores IFC.  
Versão **1.0.13** · arquivo único HTML · sem dependências · roda no navegador.

---

## O que faz

Compara capturas de tela de um mesmo elemento IFC renderizado por dois visualizadores diferentes, usando distância de Hausdorff bidirecional calculada em pixels sobre as silhuetas extraídas. Gera um relatório com:

- Mapas de diferença (Referência × A, Referência × B, A × B)
- P95 e média das distâncias em milímetros
- Piso da medição (limite de resolução) e veredito por elemento
- Detecção de elementos ausentes da captura
- Linha formatada para exportação em planilha (CSV)
- Relatório standalone em HTML

## Como usar

1. Abra `analisador_ifc.html` em qualquer navegador moderno (Chrome, Firefox, Edge).
2. Na aba **Configuração**, informe a escala da captura (mm/px) e a orientação da vista.
3. Na aba **Referência**, carregue a captura de referência (IFC spec como base).
4. Nas abas **Visualizador A** e **Visualizador B**, carregue as capturas a comparar.
5. Clique em **Comparar** para gerar o relatório.
6. Use o botão **Exportar relatório** para salvar o HTML standalone, ou **Copiar linha** para colar na planilha de resultados.

## Parâmetros principais

| Parâmetro | Valor padrão | Descrição |
|---|---|---|
| Limiar de extração | 3 | Sensibilidade da binarização da silhueta |
| Piso da medição | `max(resíduo × mm/px, 1 px)` | Limite inferior da medição |
| Observável | exclusividade ≥ 5% | Mínimo de pixels exclusivos para medir elemento |
| Medida confiável | exclusividade ≥ 50% | Elemento pouco contaminado por sobreposição |
| Tolerâncias de robustez | 0,6 / 1,0 / 1,7 × automática | Banda do teste de robustez |
| Veredito divergente | P95 > 3 × piso | Limite para classificar como divergência |
| Ausente | pegada < 10% e P95 > 50% da diagonal | Elemento não renderizado na captura |

## Requisitos

- Navegador com suporte a Canvas API e ES2020 (qualquer versão atual)
- Capturas PNG ou JPEG das vistas frontais dos elementos
- Escala conhecida (mm/px) ou resolução declarada da captura

## Histórico de versões

| Versão | Natureza da mudança |
|---|---|
| 1.0.1 | Versão inicial |
| 1.0.2 | Correções de estabilidade |
| 1.0.3–1.0.6 | Interface e tema |
| 1.0.7 | Escopo limitado a elemento único (resultado) |
| 1.0.8 | Guarda de alinhamento: recusa resultado se resíduo > 15% do quadro (resultado) |
| 1.0.9 | Correção de registro herdado ao trocar vista/resolução (resultado) |
| 1.0.10 | Coluna A×B no relatório |
| 1.0.11 | Arbitragem e linha CSV no relatório |
| 1.0.12 | Três mapas de diferença no relatório |
| 1.0.13 | Detecção de elementos ausentes da captura (resultado) |

Versões marcadas como **(resultado)** alteram valores medidos ou classificados, não apenas a apresentação.

## Contexto

Desenvolvida como artefato de pesquisa para o Trabalho de Conclusão de Curso em Engenharia Civil (UFAL, 2026), no âmbito de um estudo sobre divergências geométricas em modelos IFC entre visualizadores.

## Licença

MIT
