
## Visão Geral do Projeto 

Descrição do Funcionamento e Uso para Reprodução 
O sistema proposto é um conjunto integrado de hardware e software destinado a monitorar e 
identificar riscos em infraestruturas viárias, utilizando sensores instalados em veículos. O 
funcionamento é dividido em várias etapas: 

1. Coleta de Dados pelos Sensores: Sensores instalados nos veículos são responsáveis por 
coletar uma ampla gama de informações relevantes, como temperatura, umidade, 
velocidade, pressão dos pneus, entre outros.

3. Processamento e Transmissão de Dados: Os dados coletados pelos sensores são 
processados pelos microcontroladores ESP8266/ESP32. Esses microcontroladores 
utilizam o protocolo MQTT para transmitir os dados em tempo real para uma central de 
processamento.

5. Análise de Dados e Identificação de Riscos: Na central de processamento, algoritmos 
avançados analisam os dados recebidos para identificar potenciais riscos viários. Esses 
algoritmos podem detectar padrões, anomalias e situações de perigo com base nas 
informações coletadas pelos sensores.

7. Tomada de Decisões e Ações Corretivas: Com base na análise dos dados, a central de 
processamento pode tomar decisões automatizadas para mitigar os riscos identificados. 
Por exemplo, se um sensor detectar uma redução repentina na pressão dos pneus, a 
central pode enviar um comando para acionar um atuador que alerte o motorista ou 
ajuste a pressão dos pneus automaticamente.

9. Feedback para Motoristas e Autoridades Competentes: Além de tomar medidas 
corretivas, o sistema fornece feedback em tempo real para os motoristas sobre as 
condições do veículo e da estrada. Além disso, as autoridades competentes podem 
receber alertas automáticos sobre situações de risco, permitindo uma resposta rápida 
para garantir a segurança viária.

11. Monitoramento e Manutenção: O sistema também pode ser integrado a uma 
plataforma central de monitoramento, onde os dados agregados de múltiplos veículos 
são analisados para fornecer insights abrangentes sobre padrões, condições e 
desempenho veicular. Isso permite uma gestão eficiente da frota e a identificação de 
áreas que requerem manutenção ou melhorias. 
Software Desenvolvido e Documentação de Código 
O software desenvolvido compreende os códigos de programação para os microcontroladores 
ESP8266/ESP32, responsáveis pela comunicação MQTT e controle dos sensores e atuadores. A 
documentação de código inclui esquemas de circuito, fluxogramas e comentários detalhados 
para facilitar a compreensão e a replicação do sistema.


## Configurando sua Conta Ubidots

Para começar a enviar dados para a nuvem e visualizá-los, vamos configurar uma conta Ubidots. Ubidots é uma plataforma IoT que facilita a captura e análise de dados de sensores.

## Passo 1: Criando uma Conta Ubidots

1. Acesse ubidots.com e crie uma conta. Você terá um período de teste de 30 dias.

## Passo 2: Criando Dispositivos e Adicionando Variáveis

Agora configure um dispositivo Ubidots. Para criá-lo, vá para a seção Dispositivos (Dispositivos > Dispositivos). Crie um novo dispositivo com o nome que preferir.

https://prnt.sc/1GEfT2YPPgk5

Depois que o dispositivo for criado, crie uma nova variável renomeando a variável para "meu sensor".

https://prnt.sc/LNK2LyK7fJAN

## Passo 3: Criação de Painéis

Vamos configurar um painel do Ubidots. Para criá-lo, vá para a seção Dashboard (Dados > Dashboard)

https://prnt.sc/W01bM9kDNt19

## Passo 4: Adicionar Novos Widgets

Clique no sinal + no lado direito e em “Adicionar novo widget” e selecione seu widget.

https://prnt.sc/LBbJoNTFCrqm

Agora, selecione o tipo de widget que deseja exibir. No meu caso, escolho o “Indicador” e “Histograma”:

https://prnt.sc/1ogjxtNiKQjG

Selecione seu dispositivo e variáveis criadas anteriormente, conforme mostrado na figura abaixo.

https://prnt.sc/JDDguziXC1UJ
