# Jet Tagging: CNN vs. GNN/Particle Transformer

Este notebook é um projeto da eletiva "Aprendizado de Máquina" do Programa de Pós-Graduação em Física da Universidade do Estado do Rio de Janeiro (UERJ) que implementa e compara duas abordagens clássicas de *jet tagging* em física de altas energias.

## O que o notebook faz

Duas formas diferentes de representar um jato são construídas e comparadas a partir dos mesmos dados brutos:

1. **CNN em "imagens de jato"** — cada jato é discretizado em um grid 2D (η × φ), onde a intensidade de cada pixel corresponde ao pT depositado, de forma análoga a uma imagem de calorímetro.
2. **GNN / Particle Cloud** — cada jato é tratado como uma nuvem de partículas (os nós de um grafo), processada por uma arquitetura de atenção estilo Particle Transformer (uma versão leve, inspirada no ParticleNet/ParT).

O mesmo pipeline de pré-processamento é aplicado a **duas tarefas físicas diferentes**:

- **Quark vs. Glúon** — dataset de Komiske, Metodiev & Thaler, acessado via a biblioteca `energyflow`.
- **Top vs. QCD** — o *Top Tagging Reference Dataset* de Kasieczka, Plehn, Thompson & Russel.

No final, as duas abordagens (CNN e Transformer) são comparadas por **AUC** e por **rejeição de background a eficiência de sinal fixa**, seguido de uma análise de **interpretabilidade**: *saliency maps* para a CNN e pesos de atenção para o Transformer.

> O notebook foi desenhado para rodar em **CPU**, em um computador comum, sem GPU — por isso usa sub-amostras dos datasets completos e redes pequenas.

## Estrutura do notebook

1. Setup e configuração
2. Dataset A: Quark vs. Glúon (`energyflow`)
3. Dataset B: Top vs. QCD (Zenodo)
4. Funções utilitárias de pré-processamento (comuns às duas tarefas)
5. Construção de imagens e de nuvens de partículas
6. Modelos: CNN (estilo ResNet) e Particle-Transformer (estilo GNN de atenção)
7. Treinamento
8. Avaliação: ROC, AUC, rejeição de background
9. Interpretabilidade: saliency maps (CNN) e pesos de atenção (Transformer)
10. Conclusões

## Sobre a pasta `data/`

Essa pasta recebe os dados baixados/gerados ao rodar o notebook (cache do `energyflow` e os arquivos do Top Tagging Reference Dataset, que somam cerca de 1,7 GB). Por causa do tamanho, esses arquivos **não são versionados no repositório** — a pasta serve apenas como destino local para quem for reproduzir o notebook.

## Referências

- Komiske, Metodiev & Thaler — dataset e biblioteca **EnergyFlow**: https://energyflow.network/
- **ParticleNet** — Qu & Gouskos, *Jet Tagging via Particle Clouds*: https://arxiv.org/abs/1902.08570
- **Particle Transformer (ParT)** — Qu, Li & Qian, *Particle Transformer for Jet Tagging*: https://arxiv.org/abs/2202.03772
- **Top Tagging Reference Dataset** — Kasieczka, Plehn, Thompson & Russell, Zenodo: https://doi.org/10.5281/zenodo.2603256

## Contexto

Projeto desenvolvido para a eletiva **Aprendizado de Máquina**, do Programa de Pós-Graduação em Física da **Universidade do Estado do Rio de Janeiro (UERJ)**.
