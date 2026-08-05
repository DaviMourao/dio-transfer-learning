# 🌻 Classificador de Flores: Transfer Learning (Rosas vs Girassóis)

Fala, pessoal! 👋 

Este é o meu projeto para o desafio de Transfer Learning de Redes Neurais da DIO. 

A proposta original do desafio era usar o clássico dataset de gatos e cachorros. Porém, como eu queria testar algo um pouco diferente (e contornar uns erros de acesso 403 que estavam rolando no link original da plataforma), resolvi adaptar o problema. Criei um classificador binário de **Rosas vs Girassóis** utilizando um recorte do dataset oficial de flores do TensorFlow.

## 🛠️ Como o projeto foi construído

Todo o código foi feito em **Python** e rodado direto no **Google Colab**. 

A estratégia de Transfer Learning aqui foi utilizar a arquitetura **MobileNetV2**. Como ela já é super otimizada e foi pré-treinada no ImageNet, eu só precisei:
1. Importar o modelo base sem a última camada de classificação (`include_top=False`).
2. Congelar os pesos originais (`trainable = False`) para aproveitar tudo o que a rede já "sabe" sobre extração de características.
3. Montar o meu próprio cabeçalho no final (usando `GlobalAveragePooling2D`, um `Dropout` para dar uma segurada no overfitting, e uma camada `Dense` com ativação sigmoide) para prever se a foto é uma Rosa (0) ou um Girassol (1).

## 🚀 Como testar o código

Se quiser rodar o projeto por aí, é bem tranquilo:
1. Joga o arquivo `.ipynb` no seu Google Colab.
2. É legal mudar o ambiente de execução para usar a GPU (vai bem mais rápido).
3. Roda todas as células na sequência. 

Não precisa baixar nenhum dataset manualmente no seu computador. Eu deixei o código automatizado com comandos de terminal (`!wget` e `!tar`) que baixam os dados direto do Google Storage, criam as pastas temporárias e separam as classes de forma limpa antes de carregar o dataset no Keras.

## 📊 Resultados

O treinamento foi bem rápido. Fiz o fine-tuning apenas da última camada por **5 épocas**, e o modelo já bateu quase **85% de acurácia** na validação, com a curva de loss caindo de forma consistente. 

Eu deixei os gráficos de desempenho salvos na pasta `images/` aqui do repositório. O resultado final prova bem a ideia do Transfer Learning: dá pra conseguir classificadores muito bons gastando pouquíssimo tempo de processamento e precisando de poucos dados.
