# MegReader
A project for research in text detection and recognition using PyTorch 1.2.
Um projeto de pesquisa em detecção e reconhecimento de texto usando PyTorch 1.2.

This project is originated from the research repo, which heavily relies on closed-source libraries, of CSG-Algorithm team of Megvii(https://megvii.com).
We are in ongoing progress to transfer models into this repo gradually, released implementations are listed in [Progress](#progress).
Este projeto é originado do repositório de pesquisa, que depende fortemente de bibliotecas de código fechado, da equipe CSG-Algorithm do Megvii (https://megvii.com).
Estamos em andamento contínuo para transferir modelos para este repositório gradualmente, as implementações lançadas estão listadas em [Progress](#progress).

## Highlights

- Implementations of representative text detection and recognition methods.
- An effective framework for conducting experiments: We use yaml files to configure experiments, making it convenient to take experiments.
- Thorough logging features which make it easy to follow and analyze experimental results.
- CPU/GPU compatible for training and inference.
- Distributed training support.

- Implementações de métodos representativos de detecção e reconhecimento de texto.
- Uma estrutura eficaz para conduzir experimentos: usamos arquivos yaml para configurar experimentos, tornando-os convenientes para fazer experimentos.
- Recursos de registro completos que facilitam o acompanhamento e a análise dos resultados experimentais.
- Compatível com CPU/GPU para treinamento e inferência.
- Apoio distribuído à formação.
- 
## Install

### Requirements

`pip install -r requirements.txt`

- Python3.7
- PyTorch 1.2 and CUDA 10.0.
- gcc 5.5(Important for compiling)

### Compile cuda ops (If needed)
### Compile cuda ops (se necessário)
```
cd PATH_TO_OPS

python setup.py build_ext --inplace
```
ops may be used:
ops pode ser usado:
- DeformableConvV2 `assets/ops/dcn`
- CTC2DLoss `ops/ctc_2d`

### Configuration(optional)

Edit configurations in `config.py`.

## Training

## Treinamento

See detailed options: `python3 train.py --help`
Veja as opções detalhadas: `python3 train.py --help`

## Datasets
## Conjuntos de dados
We provide data loading implementation with annotation packed with json for quick start. 
Fornecemos implementação de carregamento de dados com anotação compactada com json para início rápido.
Also, lmdb format data are now available too.
Além disso, os dados no formato lmdb agora também estão disponíveis.
You can refer the usage in [demo](experiments/recognition/crnn-lmdb.yaml).
Você pode consultar o uso em [demo](experiments/recognition/crnn-lmdb.yaml).
Datasets used in our recognition experiments can be downloaded from [onedrive](https://megvii-my.sharepoint.cn/:f:/g/personal/wanzhaoyi_megvii_com/EjkcrpmiW6hJrUKY-0fEBRABvNMtYniUPfWLVptMmy9-6w?e=bJaYFo). The transform [script](scripts/json_to_lmdb.py) are provide to convert json format data to lmdb.
Os conjuntos de dados usados ​​em nossos experimentos de reconhecimento podem ser baixados de [onedrive](https://megvii-my.sharepoint.cn/:f:/g/personal/wanzhaoyi_megvii_com/EjkcrpmiW6hJrUKY-0fEBRABvNMtYniUPfWLVptMmy9-6w?e=bJaYFo). O [script](scripts/json_to_lmdb.py) de transformação é fornecido para converter dados do formato json para lmdb.

### Non-distributed
### Não distribuído

`python3 train.py PATH_TO_EXPERIMENT.yaml --validate --visualize --name NAME_OF_EXPERIMENT`

Following we provide some of configurations of the released recognition models:
A seguir fornecemos algumas das configurações dos modelos de reconhecimento lançados:

- CRNN: `experiments/recognition/crnn.yaml`
- 2D CTC: `experiments/recognition/res50-ppm-2d-ctc.yaml`
- Attention Decoder: `experiments/recognition/fpn50-attention-decoder.yaml`

### Distributed(recommended for multi-gpu training)
### Distribuído(recomendado para treinamento multi-gpu)
`python3 -m torch.distributed.launch --nproc_per_node=NUM_GPUS train.py PATH_TO_EXPERIMENT.yaml -d --validate`

<!--
### Setup your own dataset
-->


## Evaluating

## Avaliando
See detailed options: `python3 eval.py --help`.
Veja as opções detalhadas: `python3 eval.py --help`.

Keeping ratio tesing is recommended: `python3 eval.py PATH_TO_EXPERIMENT.yaml --resize_mode keep_ratio`
Manter o teste de proporção é recomendado: `python3 eval.py PATH_TO_EXPERIMENT.yaml --resize_mode keep_ratio`

### Model zoo
### Modelo zoo

Trained models are comming soon.
Modelos treinados estão chegando em breve.
<!--
Our trained model can be downloaded from xxx.
Nosso modelo treinado pode ser baixado de xxx.
-->

## Progress
## Progresso
### Recognition Methods
### Métodos de Reconhecimento

- [x] 2D CTC
- [x] CRNN
- [x] Attention Decoder
- [ ] Rectification

### Detection Methods
### Métodos de Detecção
- [x] Text Snake
- [x] EAST

### End-to-end
### De ponta a ponta
- [ ] Mask Text Spotter

## Contributing
## Contribuindo
[Contributing.md](CONTRIBUTING.md)
