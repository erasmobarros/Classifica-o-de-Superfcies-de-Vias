Desafio Voxar Labs 2025 - Classificação de Superfícies de Vias
Este repositório contém a solução desenvolvida para o desafio técnico de Visão Computacional da Voxar Labs (2025). O objetivo do projeto é classificar imagens de pavimentos em três categorias: Asphalt (Asfalto), Belgian Blocks (Paralelepípedos) e Off-road (Estrada de terra).

O foco principal deste projeto não é apenas a busca pela maior acurácia, mas sim a estruturação do problema, experimentação científica e análise crítica frente a um dataset altamente desbalanceado e com condições visuais desafiadoras (chuva, noite, ruído visual).

🛠 Tecnologias Utilizadas
Python 3

PyTorch & Torchvision: Construção do pipeline de dados, Data Augmentation e Transfer Learning.

Scikit-Learn: Geração de relatórios de classificação (Precision, Recall, F1-Score).

Matplotlib & Seaborn: Visualização de dados e Matrizes de Confusão.

Google Colab: Ambiente de desenvolvimento e treinamento com aceleração de GPU.

📊 O Dataset e seus Desafios
O conjunto de dados simula cenários do mundo real para sistemas de assistência ao condutor (ADAS), apresentando:

Heterogeneidade Visual: Câmeras diferentes, sombras, reflexos de asfalto molhado e capturas noturnas.

Desbalanceamento Severo: A classe Asphalt é amplamente majoritária, enquanto Belgian Blocks possui um número escasso de amostras.

🚀 Metodologia e Experimentos
O projeto foi estruturado em três etapas principais de modelagem:

1. Solução Baseline (Transfer Learning)
Foi utilizada a arquitetura ResNet-18 pré-treinada no ImageNet, substituindo apenas a camada final (Classificador Linear).

Resultado: Alta acurácia global (85%), porém com um forte viés para a classe majoritária. O baixo Recall (0.19) na classe minoritária expôs a "acurácia ilusória" causada pelo desbalanceamento.

2. Experimento 1: Ponderação de Perda (Weighted Loss)
Substituição da função de custo padrão por uma CrossEntropyLoss com pesos inversamente proporcionais à frequência das classes.

Resultado: Melhoria notável na identificação da classe minoritária. Penalizar matematicamente os erros nas classes mais raras forçou o modelo a aprender suas características, agregando robustez à rede.

3. Experimento 2: Data Augmentation
Adição de transformações aleatórias (ColorJitter, RandomRotation) para simular condições climáticas e variações de iluminação.

Resultado: Houve queda no desempenho da classe Belgian Blocks.

Análise: Devido à extrema falta de amostras reais dessa classe, transformações agressivas de brilho e contraste acabaram descaracterizando as texturas autênticas das pedras, confundindo o modelo. Isso demonstra que Data Augmentation sintético não substitui a necessidade de dados originais de qualidade em classes sub-representadas.

💻 Como Executar o Projeto
Faça o clone deste repositório:

Bash
git clone https://github.com/SEU_USUARIO/NOME_DO_REPOSITORIO.git
O projeto foi desenhado para rodar perfeitamente no Google Colab. Basta fazer o upload do arquivo notebook_revisado.ipynb para a plataforma.

Certifique-se de alterar a variável data_dir no notebook para apontar para o local onde as imagens do dataset estão salvas no seu Google Drive:

Python
data_dir = '/content/drive/MyDrive/caminho/para/o/dataset'
Vá em Ambiente de Execução > Alterar o tipo de ambiente de execução e selecione T4 GPU para acelerar o treinamento.

Execute as células sequencialmente.

📌 Próximos Passos
Caso houvesse mais tempo para iterações futuras, os próximos passos incluiriam:

Aplicação de Oversampling para equilibrar a distribuição de imagens no DataLoader.

Implementação de Focal Loss para reduzir o peso de exemplos "fáceis" de classificar durante o treino.

Fine-tuning gradual (descongelamento em etapas das camadas da ResNet).

Projeto desenvolvido por Erasmo Barros como submissão técnica para a Voxar Labs.
