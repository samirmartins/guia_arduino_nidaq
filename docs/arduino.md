#O que é esse guia?
Manual rápido para trabalho com placas Arduino, além de instalação e configurações do Arduino IDE, e plataformas de simulação como TinkerCAD.

#Arduino IDE
Arduino IDE é um software onde é possível desenvolver e 
compilar códigos em linguagem C/C++, e também enviarmos esse código para a
placa, onde ela funcionará de forma independente, desconectada do computador.
Para o download do software basta acessar https://www.arduino.cc/en/software/

#Desenvolvimento do projeto 
Existem diversos tipos de placas Arduino no mercado, e cada uma 
apresenta diferenças em suas portas de entrada e saída, aqui temos alguns
comandos básicos genéricos a quaisquer arduinos e que quase sempre são utilizados 
````python
    pinMode(pin, MODE): Define o modo de funcionamento de um pino como entrada (INPUT) ou saída (OUTPUT).
    digitalRead(pin): Lê o estado de um pino digital (HIGH ou LOW). 
    digitalWrite(pin, STATE): Escreve um valor digital (HIGH ou LOW) num pino digital. 
    analogRead(pin): Lê um valor analógico de um pino analógico. 
    analogWrite(pin, value): Escreve um valor analógico (0-255) num pino PWM (Pulse Width Modulation). 
    delay(milliseconds): Pausa o programa por um determinado número de milissegundos. 
    Serial.begin(baudrate): Inicializa a comunicação serial com uma taxa de bits por segundo especificada. 
    Serial.print(data): Imprime dados através da comunicação serial. 
    Serial.println(data): Imprime dados e adiciona uma nova linha no final através da comunicação serial. 
````
    
    
Para definir quais entradas tem o arduino que você está trabalhando abra o 
datasheet específico do mesmo.

#Exemplo de código


#Obtenção de dados 









