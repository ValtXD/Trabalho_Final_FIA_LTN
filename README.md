# Projeto: Raciocínio Neuro-Simbólico com CLEVR e LTN

## Sobre o Projeto

Este projeto implementa um sistema neuro-simbólico usando **Logic Tensor Networks (LTN)** para raciocínio visual sobre cenas CLEVR. O sistema combina aprendizado profundo com lógica formal para entender relações espaciais entre objetos.

---

<span style="font-weight: bold; font-size: 16px; color: #333;">Alunos</span>

<table style="border-collapse: collapse; width: 100%;">
  <tr>
    <th align="left" style="padding: 8px; border-bottom: 1px solid #ddd;">Nome</th>
    <th align="left" style="padding: 8px; border-bottom: 1px solid #ddd;">Email</th>
  </tr>
  <tr>
    <td style="padding: 8px; border-bottom: 1px solid #ddd;">Beatriz Christine Azevedo Batista</td>
    <td style="padding: 8px; border-bottom: 1px solid #ddd;">beatriz.batista@icomp.ufam.edu.br</td>
  </tr>
  <tr>
    <td style="padding: 8px; border-bottom: 1px solid #ddd;">Francisco Felipe Barros dos Santos</td>
    <td style="padding: 8px; border-bottom: 1px solid #ddd;">francisco.santos@icomp.ufam.edu.br</td>
  </tr>
  <tr>
    <td style="padding: 8px; border-bottom: 1px solid #ddd;">Ivan Marcos Freitas dos Santos</td>
    <td style="padding: 8px; border-bottom: 1px solid #ddd;">ivanm.santos@icomp.ufam.edu.br</td>
  </tr>
  <tr>
    <td style="padding: 8px; border-bottom: 1px solid #ddd;">Matheus Carvalho Reges</td>
    <td style="padding: 8px; border-bottom: 1px solid #ddd;">matheus.reges@icomp.ufam.edu.br</td>
  </tr>
</table>

---

## Conceitos Teóricos

### 1. Neuro-Simbólico (NeSy) e Logic Tensor Networks (LTN)

### Neuro-Simbólico (NeSy)
A abordagem neuro-simbólica combina as capacidades de aprendizado das redes neurais com o poder de raciocínio da lógica simbólica. Enquanto as redes neurais aprendem padrões complexos a partir dos dados, a lógica formal permite expressar conhecimento de domínio, restrições e regras de inferência.

### Logic Tensor Networks (LTN)
LTN é um framework que "tensoriza" a lógica de primeira ordem, permitindo que predicados sejam representados como redes neurais e que fórmulas lógicas sejam avaliadas de forma diferenciável. Isso possibilita o treinamento end-to-end de sistemas que aprendem tanto os conceitos quanto as regras lógicas que os relacionam.

**Principais componentes:**
- **Predicados**: Redes neurais que aprendem conceitos
- **Conectivos lógicos**: Operações fuzzy sobre tensores
- **Quantificadores**: Agregações sobre domínios de objetos
- **Treinamento**: Maximização da satisfação lógica (satAgg)

---

### 2. Dataset CLEVR Simplificado

Baseado no dataset CLEVR original (Compositional Language and Elementary Visual Reasoning), implementamos uma versão simplificada:

#### Estrutura do Vetor (11 features):
| Posição | Índice | Descrição |
|---------|--------|-----------|
| Posição | 0-1 | Coordenadas (x, y) normalizadas |
| Cor | 2-4 | One-hot: [Red, Green, Blue] |
| Forma | 5-9 | One-hot: [Circle, Square, Cylinder, Cone, Triangle] |
| Tamanho | 10 | Binário: 0.0=Pequeno, 1.0=Grande |

#### Características:
- 25 objetos por cena
- Posições aleatórias no plano 2D
- Combinações aleatórias de cor/forma/tamanho
- Foco em raciocínio espacial e composicional

---

## Resultados Experimentais

### 3. Satisfação das Fórmulas no Conjunto de Teste

| Fórmula | Descrição | Satisfação Média |
|---------|-----------|------------------|
| `lastOnTheLeft` | Objeto mais à esquerda de todos | 0.0459 ± 0.0229 |
| `lastOnTheRight` | Objeto mais à direita de todos | 0.0483 ± 0.0046 |
| `exists_left_of_all_squares` | Objeto à esquerda de todos os quadrados | 0.5874 ± 0.0430 |
| `exists_small_below_cylinder_left_of_square` | Pequeno abaixo de cilindro e à esquerda de quadrado | 0.0182 ± 0.0110 |
| `exists_green_cone_in_between` | Cone verde entre dois objetos | 0.0002 ± 0.0000 |

### 4. Resultados de 5 Execuções com Datasets Aleatórios

#### Métricas Consolidadas (Médias ± Desvio Padrão):

| Métrica | Média | Desvio Padrão |
|---------|-------|---------------|
| **Satisfação Agregada (sat_agg)** | 0.9418 | ± 0.0040 |
| **Acurácia** | 1.0000 | ± 0.0000 |
| **Precisão** | 1.0000 | ± 0.0000 |
| **Recall** | 1.0000 | ± 0.0000 |
| **F1-Score** | 1.0000 | ± 0.0000 |

#### Tabela Detalhada por Execução:

| Execução | sat_agg | lastOnTheLeft | lastOnTheRight | left_of_all_squares | small_below_cylinder | green_cone_between | Acurácia | Precisão | Recall | F1-Score |
|----------|---------|---------------|----------------|---------------------|----------------------|-------------------|----------|----------|--------|----------|
| 1 | 0.9345 | 0.0007 | 0.0398 | 0.5157 | 0.0002 | 0.0002 | 1.0000 | 1.0000 | 1.0000 | 1.0000 |
| 2 | 0.9407 | 0.0501 | 0.0468 | 0.5631 | 0.0112 | 0.0002 | 1.0000 | 1.0000 | 1.0000 | 1.0000 |
| 3 | 0.9438 | 0.0606 | 0.0513 | 0.6029 | 0.0222 | 0.0002 | 1.0000 | 1.0000 | 1.0000 | 1.0000 |
| 4 | 0.9449 | 0.0598 | 0.0517 | 0.6230 | 0.0273 | 0.0002 | 1.0000 | 1.0000 | 1.0000 | 1.0000 |
| 5 | 0.9451 | 0.0583 | 0.0518 | 0.6322 | 0.0298 | 0.0002 | 1.0000 | 1.0000 | 1.0000 | 1.0000 |

---

### Evolução do Treinamento
Durante o treinamento, observamos uma melhoria consistente na satisfação:
- **Época 0**: 56.48% de satisfação
- **Época 100**: 71.98% de satisfação  
- **Época 200**: 82.66% de satisfação
- **Época 275**: 87.36% de satisfação

---

## Arquitetura do Sistema

### Predicados Implementados:

#### Predicados Unários (Formas e Tamanhos):
```python
isCircle = ltn.Predicate(UnaryPredicate())
isSquare = ltn.Predicate(UnaryPredicate())
isCylinder = ltn.Predicate(UnaryPredicate())
isCone = ltn.Predicate(UnaryPredicate())
isTriangle = ltn.Predicate(UnaryPredicate())
isSmall = ltn.Predicate(UnaryPredicate())
isBig = ltn.Predicate(UnaryPredicate())
```

---

## Análise dos Resultados

### Pontos Fortes
1. **Alta Performance**: 94.2% de satisfação geral da base de conhecimento
2. **Classificação Perfeita**: 100% de acurácia na identificação de formas e tamanhos
3. **Consistência**: Baixo desvio padrão entre execuções (robustez)
4. **Interpretabilidade**: Fórmulas lógicas tornam o raciocínio transparente

### Insights
- O modelo aprende efetivamente **conceitos básicos** (formas, tamanhos)
- **Relações simples** são bem capturadas (esquerda/direita, acima/abaixo)
- **Composição de relações** representa um desafio maior
- A abordagem LTN mostra **viabilidade** para raciocínio visual composicional

---

## Conclusões

Este trabalho demonstrou com sucesso a aplicação de Logic Tensor Networks para raciocínio neuro-simbólico sobre cenas visuais no estilo CLEVR. Os resultados mostram que:

1. **Aprendizado Efetivo**: O modelo aprende conceitos visuais e relações espaciais básicas
2. **Integração Bem-sucedida**: A combinação entre aprendizado profundo e lógica formal é viável
3. **Desafios de Complexidade**: Fórmulas complexas requerem abordagens mais sofisticadas
4. **Potencial de Aplicação**: A metodologia é promissora para tarefas que exigem raciocínio composicional

O projeto abre caminho para investigações futuras em arquiteturas mais avançadas, datasets mais complexos e aplicações em problemas do mundo real que exigem integração entre percepção visual e raciocínio lógico.

---
### Passo a Passo:

1. **Acesse o Google Colab:**
   - Vá para [colab.research.google.com](https://colab.research.google.com)

2. **Carregue o notebook:**
   - Faça o download do arquivo `.ipynb`
   - Clique em "Upload" e selecione o arquivo `trabalho_3_FIA_versão1_18_Fran.ipynb`
   - **OU** copie o link do GitHub diretamente no Colab

3. **Execute todas as células:**
   - `Runtime` → `Run all`
   - Aguarde a instalação automática das dependências
