# Guia de Uso - Placas NIDAQ + Python

## O que é este guia?

Este guia foi escrito para novos membros do GCOM ([Grupo de Controle e Modelagem](https://www.ufsj.edu.br/gcom)). O objetivo
desta seção é desmistificar a utilização de placas de aquisição de dados da National Instruments (NIDAQ - National 
Instruments Data Acquisition USB Devices) utilizando Python como linguagem de programação.

- **OBSERVAÇÃO 1:** para utilizar este guia, o usuário deverá estar familiarizado com a linguagem Python,
bem como instalação de bibliotecas. 
- **OBSERVAÇÃO 2:** a biblioteca nidaqmx será usada como base neste guia. Para instalá-la, use o comando: 

````python
pip install nidaqmx
````

Aqui expressamos publicamente nossa gratidão aos autores da biblioteca.

- **OBSERVAÇÃO 3:** o driver USB da placa de aquisição de dados precisa estar instalado. No momento da escrita deste 
guia, o download podia ser realizado [por este link](https://www.ni.com/en/support/downloads/drivers/download.ni-daq-mx.html?srsltid=AfmBOoqR5dNImzE-uENtu_rWsn18H7xPUaxoC6IlAsGM96JzoROllMhs#565026), após um 
registro gratuito em www.ni.com. Alternativamente, o usuário pode instalar drivers utilizando também o comando:

````python
python -m nidaqmx installdriver
````

Recomendamos a primeira opção como o padrão.

**IMPORTANTE:** esta é uma versão muito resumida para uso rápido. Maiores detalhes podem ser encontrados (em inglês) em 
[https://pypi.org/project/nidaqmx/](https://pypi.org/project/nidaqmx/)

## Tarefas (Task)

Uma tarefa é um conjunto de canais virtuais com temporização e outras propriedades. Resumidamente, 
são necessárias tarefas para aquisição e envio de dados. [Maiores informações aqui.](https://www.ni.com/docs/en-US/bundle/ni-daqmx/page/tasksnidaqmx.html)

Para criar uma tarefa, use o seguinte comando: 

````python
import nidaqmx # Importa a biblioteca 

with nidaqmx.Task() as task: # Cria a tarefa 
    pass # Aqui você deve digitar o código que deverá ser executado naquela tarefa.
````

## Canais Virtuais


## Timing

## Aquisição de dados - Analog Input

### DIFF, RSE e NRSE

### Analog Input - Exemplo 

## Envio de dados - Analog Output

### Analog Output - Exemplo 