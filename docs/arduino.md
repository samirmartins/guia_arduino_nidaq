#O que é esse guia?
Manual rápido para trabalho com placas Arduino, além de instalação e configurações do Arduino IDE, 
e plataformas de simulação como TinkerCAD.

#Arduino IDE
##Instalação
Arduino IDE é um software onde é possível desenvolver e 
compilar códigos em linguagem C/C++, e também enviarmos esse código para a
placa, onde ela funcionará de forma independente, desconectada do computador.
Para o download do software basta acessar <https://www.arduino.cc/en/software/>
##Configurações
Após instalar com sucesso o ‘software’ será necessário conectar o microcontrolador ao computador, você
precisará selecionar qual o modelo de arduino está sendo utilizado (ex: Arduino UNO, Arduino NANO), para isto
basta ir dentro do aplicativo no menu ferramentas(tools) e selecionar a opção placa, dentro dela estará listado o
modelo de seu equipamento.


![Seleção do modelo](./img/ArduinoMarkdown1.jpeg)


Depois disso será necessário indicar a IDE qual porta está sendo utilizada pela sua placa, par isso basta 
ir novamente ao menu ferramentas, porém dessa vez selecione a opção porta. 
Você verá uma lista de portas disponíveis. Geralmente, a porta correta será identificada com o nome da
placa ao lado (ex: "COM3 (Arduino Uno)"). Se houver dúvidas, desconecte a placa, verifique quais portas 
sumiram da lista e conecte-a novamente para confirmar.

![Seleção do modelo](./img/ArduinoMarkdown2.jpg)


Embora a instalação do Arduino IDE em sistemas operacionais modernos inclua geralmente os drivers 
necessários para placas originais, placas "clones" ou similares podem exigir a instalação manual de um
driver específico, para que a porta de comunicação seja reconhecida. Para isso
verifique o chip próximo à porta USB da sua placa. Procure por nomes como "CH340G" ou "FT232RL". 
Em seguida, baixe e instale o driver correspondente para o seu sistema operacional.

![Seleção do modelo](./img/ArduinoMarkdown3.jpeg)

![Seleção do modelo](./img/ArduinoMarkdown4.jpg)


Para o desenvolvimento de quaisquer códigos dentro do arduino bibliotecas serão de suma importância, 
para importá-las e conseguir trabalhar de maneira mais fácil é necessário, ir ao menu Sketch > Incluir 
biblioteca > Gerenciar bibliotecas, então utilizar a barra de busca pela biblioteca desejada, selecione-a e
clique em instalar.

![Seleção do modelo](./img/ArduinoMarkdown5.jpg)

#Desenvolvimento do projeto 
Existem diversos tipos de placas Arduino no mercado, e cada uma 
apresenta diferenças em suas portas de entrada e saída, aqui temos alguns
comandos básicos genéricos a quaisquer arduinos e que quase sempre são utilizados 
```c
    pinMode(pin, MODE): Define o modo de funcionamento de um pino como entrada (INPUT) ou saída (OUTPUT).
    digitalRead(pin): Lê o estado de um pino digital (HIGH ou LOW). 
    digitalWrite(pin, STATE): Escreve um valor digital (HIGH ou LOW) num pino digital. 
    analogRead(pin): Lê um valor analógico de um pino analógico. 
    analogWrite(pin, value): Escreve um valor analógico (0-255) num pino PWM (Pulse Width Modulation). 
    delay(milliseconds): Pausa o programa por um determinado número de milissegundos. 
    Serial.begin(baudrate): Inicializa a comunicação serial com uma taxa de bits por segundo especificada. 
    Serial.print(data): Imprime dados através da comunicação serial. 
    Serial.println(data): Imprime dados e adiciona uma nova linha no final através da comunicação serial. 
```

Para definir quais entradas tem o arduino o qual você está trabalhando abra o 
datasheet específico do mesmo.
#Obtenção de dados
#Simulação
Ao trabalharmos com circuitos elétricos/eletrônicos uma etapa crucial é a simulação, já que com ela é possível
ter uma estimativa dos valores de saída desejados e por consequência conseguiremos adaptar os equipamentos
para que eles funcionem sem nenhum risco de acidente.
Dentre os diversos ambientes de simulação este guia abordará o básico sobre o [TinkerCAD](https://www.tinkercad.com)
Localize a Biblioteca: No lado esquerdo da tela, você encontrará a biblioteca de componentes. Essa biblioteca 
contém uma ampla variedade de componentes eletrônicos, categorizados por tipo.
Explore as Categorias: Clique nas guias na parte superior da biblioteca para navegar por diferentes 
categorias de componentes, como resistores, LEDs, fios, fontes de alimentação, etc.
Encontre o Componente Desejado: Utilize a barra de pesquisa ou navegue pelas categorias para encontrar o 
componente específico que você precisa.
Clique no Componente: Clique no ícone do componente para selecioná-lo.
Arraste e Solte na Área de Trabalho: Pressione o botão esquerdo do mouse e arraste o componente selecionado
para a área de trabalho no lado direito da tela. Solte o botão do mouse para posicionar o componente onde 
deseja.
#









