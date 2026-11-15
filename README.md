# Projsin: Projeto de Sinalização sobre ortofoto

Aplicativo web (um único arquivo, `index.html`) para verificar, sobre a ortofoto de drone de uma rodovia, se a plataforma comporta a seção-tipo da sinalização definitiva:

- faixa de segurança (padrão 0,60 m)
- N faixas de rolamento (padrão 2 × 3,60 m)
- acostamento mínimo remanescente (padrão 2,50 m)

O aplicativo desenha as linhas de projeto (bordo esquerdo, LMS tracejada e bordo da última faixa) e pinta o acostamento resultante de verde (atende) ou vermelho (não atende). Para cada estaca ele mostra a largura da plataforma, o acostamento que sobra e a largura máxima de faixa que ainda manteria o acostamento mínimo.

## Como usar

1. Abra o `index.html` no Chrome ou no Edge. Não precisa de instalação nem de servidor.
2. **Imagem**: arraste a ortofoto. Formatos aceitos:
   - GeoTIFF: a escala é lida do próprio arquivo;
   - JPG ou PNG junto com o arquivo `.jgw`/`.pgw`/`.tfw`: selecione os dois arquivos juntos;
   - JPG ou PNG sem georreferência: defina a escala no passo 2.
3. **Escala**: informe o GSD (cm/pixel) do ortomosaico ou calibre pela distância entre dois pontos conhecidos.
4. **Bordos**: trace o *bordo de referência* (lado do canteiro, onde fica a faixa de segurança) e depois o *bordo externo* (onde termina o acostamento). Clique ponto a ponto. Duplo clique ou Enter conclui.
5. **Seção-tipo**: ajuste larguras, nº de faixas, km inicial e intervalo de estacas.
6. **Exportar**: PNG com o projeto desenhado, CSV das estacas e projeto em JSON (para reabrir depois).

### Convenção de medida

- *Entre eixos* (padrão): 0,60 + 3,60 + 3,60 = 7,80 m até o eixo da linha de bordo. O acostamento é medido desse eixo até o bordo externo.
- *Livres entre linhas*: a largura de cada linha (padrão 0,15 m) é somada às faixas.

## Precisão: drone e satélite

| Fonte | Resolução típica | Erro absoluto típico | Serve para decidir 10–20 cm? |
|---|---|---|---|
| Google Earth / satélite comum | 30–60 cm/px | 1–5 m de posição | Não |
| Satélite de altíssima resolução (30 cm, pago) | 30 cm/px | ±0,3–0,6 m em larguras | Só para triagem |
| Foto única de drone, nadiral | 1–3 cm/px | 1–3 % (lente, relevo, inclinação) | Com cuidado |
| Ortomosaico de drone com RTK/PPK ou pontos de controle | 1–3 cm/px | 2–5 cm | Sim |

Uma *largura* medida na mesma imagem depende pouco do erro de posição absoluto e muito do GSD e da nitidez do bordo. A recomendação é ortomosaico com GSD ≤ 3 cm, gerado em Pix4D, Metashape, DroneDeploy ou WebODM, com RTK ou pelo menos 3 pontos de controle por km. Confira a escala medindo em campo uma ou duas larguras (por exemplo, de uma faixa existente) e comparando com a ferramenta **Medir**.

Ortomosaicos muito grandes são reduzidos para cerca de 64 megapixels no navegador. Para manter a resolução original, recorte trechos de 300 a 500 m.
