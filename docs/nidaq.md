# Guia de Uso - Placas NIDAQ + Python

## O que é este guia?

Este guia foi escrito para novos membros do GCOM ([Grupo de Controle e Modelagem](https://www.ufsj.edu.br/gcom)). O objetivo
desta seção é desmistificar a utilização de placas de aquisição de dados da National Instruments (NIDAQ - National 
Instruments Data Acquisition USB Devices) utilizando Python como linguagem de programação.

- **OBSERVAÇÃO 1:** para utilizar este guia, o usuário deverá estar familiarizado com a linguagem Python,
bem como instalação de bibliotecas. 
- **OBSERVAÇÃO 2:** a biblioteca nidaqmx será usada como base neste guia. Para instalá-la, use o comando: 

```python
pip install nidaqmx
```

Aqui expressamos publicamente nossa gratidão aos autores da biblioteca.

- **OBSERVAÇÃO 3:** o driver USB da placa de aquisição de dados precisa estar instalado. No momento da escrita deste 
guia, o download podia ser realizado [por este link](https://www.ni.com/en/support/downloads/drivers/download.ni-daq-mx.html?srsltid=AfmBOoqR5dNImzE-uENtu_rWsn18H7xPUaxoC6IlAsGM96JzoROllMhs#565026), após um 
registro gratuito em www.ni.com. Alternativamente, o usuário pode instalar drivers utilizando também o comando:

```python
python -m nidaqmx installdriver
```

Recomendamos a primeira opção como o padrão.

**IMPORTANTE:** esta é uma versão muito resumida para uso rápido. Maiores detalhes podem ser encontrados (em inglês) em 
[https://pypi.org/project/nidaqmx/](https://pypi.org/project/nidaqmx/)

## Tarefas (Task)

Uma tarefa é um conjunto de canais virtuais com temporização e outras propriedades. Resumidamente, 
são necessárias tarefas para aquisição e envio de dados. [Maiores informações aqui.](https://www.ni.com/docs/en-US/bundle/ni-daqmx/page/tasksnidaqmx.html)

Para criar uma tarefa, use o seguinte comando: 

```python
import nidaqmx # Importa a biblioteca 

with nidaqmx.Task() as task: # Cria a tarefa 
    pass # Aqui você deve digitar o código que deverá ser executado naquela tarefa.
```

## Canais Virtuais

Um canal virtual é um pedaço de software que encapsula o canal físico juntamente com 
informações a seu respeito (faixa de medição, configuração dos terminais e outras) que
formatam os dados. Por outro lado, um canal físico é o terminal em que você mede ou gera
sinais analógicos ou digitais, sendo que um canal físico pode incluir mais que um terminal (
caso de entrada analógica diferencial).

**IMPORTANTE:** cada canal físico tem um nome único (exemplos: Dev1/ao1) a depender do nome 
do dispositivo (configurável via NI-MAX). Para maiores informações [acesse aqui](https://www.ni.com/docs/en-US/bundle/ni-daqmx/page/chans.html).

A seguir um exemplo de código de como adicionar um canal de entrada analógica a uma tarefa, configurando
range e lendo um dado: 

```python
import nidaqmx

with nidaqmx.Task() as task:
    task.ai_channels.add_ai_voltage_chan("Dev1/ai0", min_val=-10.0, max_val=10.0)
    task.read()
AIChannel(name=Dev1/ai0)
0.54875412354412544
```

Para adicionar múltiplos canais a uma tarefa e configurá-los: 

```python
import nidaqmx

with nidaqmx.Task() as task:
    task.ai_channels.add_ai_voltage_chan("Dev1/ai0", min_val=-5.0, max_val=5.0)
    task.ai_channels.add_ai_voltage_chan("Dev1/ai1", min_val=-10.0, max_val=10.0)
    task.read()
AIChannel(name=Dev1/ai0)
AIChannel(name=Dev1/ai1)
[1.12345897042644564, -2.1234589701454564]
```

## Temporização da Sessão e Período de Amostragem

Você pode usar a placa de aquisição de dados da National para computar o tempo entre duas 
amostras (período de amostragem) ou o próprio clock de seu computador. Esteja ciente que a utilização
de placas de aquisição de dados para temporização da sessão/cômputo do período de amostragem 
(temporização por hardware) é significativamente mais eficiente que a utilização de temporização 
por software (pelo computador).

Para adquirir sinais utilizando temporização por harware:

```python
import nidaqmx
from nidaqmx.constants import AcquisitionType, READ_ALL_AVAILABLE

with nidaqmx.Task() as task:
    task.ai_channels.add_ai_voltage_chan("Dev1/ai0")
    task.timing.cfg_samp_clk_timing(1000.0, sample_mode=AcquisitionType.FINITE, samps_per_chan=10)
    data = task.read(READ_ALL_AVAILABLE)
    print("Acquired data: [" + ", ".join(f"{value:f}" for value in data) + "]")

AIChannel(name=Dev1/ai0)
Acquired data: [-0.149693, 2.869503, 4.520249, 4.704886, 2.875912, -0.006104, -2.895596, -4.493698, -4.515671, -2.776574]
```

### DIFF, RSE e NRSE

Há uma diferença entre métodos de coleta de dados. Usando a configuração terminal 

- **DIFF (Differential)**: os terminais físicos vão medir a diferença de potencial
entre dois terminais físicos (AI+ e AI-). Esta é preferível quando se tem ruído de modo comum. 
Evita, ainda, loops de terra 
- **RSE (Referenced Single-Ended)**: nesta configuração usa-se o terra do chassi do dispositivo DAQ
como referência. Utiliza apenas uma entrada física por canal (ao contrário do DIFF, que usa duas).
Entretanto, apresenta maior susceptibilidade a ruído de modo comum e loops de terra.
- **NRSE (Non-Referenced Single-Ended)**: usa uma referência de terra compartilhado por todos os canais. Não possui, 
necessariamente, o terra do chassi do dispositivo. Permite uma conexão específica para o terra para todos os canais.

Exemplo: 

```python
import nidaqmx
from nidaqmx.constants import AcquisitionType, READ_ALL_AVAILABLE, TerminalConfiguration

with nidaqmx.Task() as task:

	# ATENÇÃO: DESCOMENTE UMA DAS LINHAS ABAIXO, CONFORME CONFIGURAÇÃO TERMINAL DESEJADA
    #task.ai_channels.add_ai_voltage_chan("Dev1/ai0", terminal_config=TerminalConfiguration.DIFF)
    #task.ai_channels.add_ai_voltage_chan("Dev1/ai1", terminal_config=TerminalConfiguration.RSE)
	#task.ai_channels.add_ai_voltage_chan("Dev1/ai2", terminal_config=TerminalConfiguration.NRSE)
    
    task.timing.cfg_samp_clk_timing(1000.0, sample_mode=AcquisitionType.FINITE, samps_per_chan=10)
    data = task.read(READ_ALL_AVAILABLE)
    print("Acquired data: [" + ", ".join(f"{value:f}" for value in data) + "]")

AIChannel(name=Dev1/ai0)
Acquired data: [-0.149693, 2.869503, 4.520249, 4.704886, 2.875912, -0.006104, -2.895596, -4.493698, -4.515671, -2.776574]
```

## Envio de dados - Analog Output

Podemos usar canais de saída para gerar sinais de tensão pela placa de aquisição de 
dados da National. Abaixo um exemplo de como utilizar o canal analógico ao0 (analog output 0)
para enviar um sinal de tensão utilizando uma tarefa com o método **write**:

```python
import nidaqmx

with nidaqmx.Task() as task:
    task.ao_channels.add_ao_voltage_chan("Dev1/ao0")
    task.write([1.1, 2.2, 3.3, 4.4, 5.5], auto_start=True)
```