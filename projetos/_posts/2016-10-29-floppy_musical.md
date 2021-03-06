---
layout:     post
type:       projeto
hidden:     true
title:      "Floppy Musical"
date:       2016-10-29
author:     "Marcelo Schmitt"
author_url: "https://github.com/marceloschmitt1"
img:        "assets/images/projetos/2016-10-29-floppy_musical/floppy.jpg"
img_url:    ""

redirect_from:
 - "projetos/floppy-musical"
 - "projetos/floppy-musical/"
---

Este post descreve como montar o projeto MoppyAdvanced de [SammyIAm](https://github.com/SammyIAm), que chamaremos simplesmente de floppy musical ou moppy.

<div class="img-container">
  <figure>
    <img class="large" src="{{ site.baseurl }}/assets/images/projetos/2016-10-29-floppy_musical/floppy.jpg">
    <figcaption>&nbsp;</figcaption>
  </figure>
</div>

<iframe class="youtube" src="https://www.youtube.com/embed/hsN9MINXFiQ?rel=0" frameborder="0" allowfullscreen></iframe>

<iframe class="youtube" src="https://www.youtube.com/embed/Z7V2LiwLtbM?rel=0" frameborder="0" allowfullscreen></iframe>

Primeiramente, este projeto é baseado no projeto do Sammy que você encontra [aqui](https://github.com/SammyIAm/Moppy). Além de baixar os arquivos do projeto você precisará da biblioteta [TimerOne](https://code.google.com/archive/p/arduino-timerone/downloads) para Arduino e do JDK 7 (ou mais atual) instalado. Sugerimos que você use o [NetBeans](https://netbeans.org/) para compilar o projeto Java que está na pasta `Moppy/Java/MoppyDesk` já que o projeto foi desenvolvido nessa IDE. Não se esqueça de incluir a biblioteca `nrjavaserial` (que está na pasta `Moppy/Java/SerialDrivers`) ao projeto quando abri-lo com o NetBeans.

#### Pontos importantes na hora de montar o projeto (hardware)

Além dos pinos `Step` e `Control` que devem ser ligados ao Arduino conforme descrito pelo Sammy, você também deve ligar os pinos 11 e 12 (pinos em vermelo na imagem) em curto no `floppy/driver` de disquete para que ele ligue!

<div class="img-container">
  <figure>
    <img src="{{ site.baseurl }}/assets/images/projetos/2016-10-29-floppy_musical/pinagem.jpg">
    <figcaption>&nbsp;</figcaption>
  </figure>
</div>

Você perceberá que o led indicador de ligado e desligado ficará ligado quando o floppy estiver energizado e com os pinos 11 e 12 em curto. Se por algum motivo o pino 11 não estiver presente, você pode conectar o pino 12 a qualquer um dos pinos de número ímpar que também deve funcionar. Isso por que na verdade todos os pinos de número ímpar estão em curto no floppy.

Outra coisa importante a se saber é a voltagem de operação e a corrente necessária para alimentar cada floppy. Por padrão cada floppy opera a 5 volts e, segundo [este tópico](http://forum.arduino.cc/index.php?topic=152419.0), cada um deve ser alimentado com uma corrente que pode variar de 0,3 a 0,7 ampere. Se você tiver uma fonte de computador, você pode usá-la para alimentar o(s) floppy(s) sem se preocupar com esse tipo de coisa. Basta ligá-lo(s) na fonte exatamente como você faria se o(s) estivesse instalando em um computador. Porém, se você não tiver uma fonte de computador e/ou tiver muitos floppys, você provavelmente vai precisar usar uma fonte convencional e então deverá atentar para as especificações de voltagem e corrente deles. Por exemplo, para o projeto que montamos com 4 floppys foi necessária uma fonte de 5 volts e 2 amperes para alimentá-los.

Por último, certifique-se de ligar o Arduino e os floppys no mesmo terra. Isso pode ser feito ligando um pino GND do Arduino a um pino de número ímpar no floppy (Sammy recomenda que seja o pino abaixo do pino STEP, mas o projeto que montamos funcionou ligando o GND a qualquer pino ímpar). Se os pinos ímpares de todos os floppys estiverem em curto, basta ligar um desses pinos numa entrada GND da Arduino (na foto acima fizemos isso com um fio roxo).

#### O Moppy Control Application (programa Java)

As principais funções que usamos no modo MIDI File foram:

- `Moppy Serial`: você seleciona a porta serial do dispositivo que se comunica com o(s) floppy(s) (no caso, a porta serial na qual a sua placa Arduino está conectada);
- `Load Sequence`: lhe permite selecionar um arquivo de audio no formato MIDI para execução;
- `Enable Drive-Pooling`: na estratégia Straight-Throught que executa o arquivo MIDI no estilo um canal MIDI para um floppy e na estratégia Round-Robin que executa o arquivo MIDI alternando a execução dos canais MIDI entre os floppys livres;
- `Connect`, `Start` e `Stop/Reset` para iniciar a conexão com o Arduino e com os floppys, iniciar a execução da música e para/reiniciar a música, respectivamente.

No modo MIDI IN Port você pode executar entradas no formato MIDI diretamente nos floppys. Por exemplo, se você tiver um teclado com saída no formato MIDI, você pode conectá-lo ao seu computador e ter as notas tocadas nele reproduzidas pelos floppys.

#### Arquivos MIDI

O projeto moppy tem três arquivos MIDI para teste na pasta `Moppy/Java/MoppyDesk/samplesongs`. Mais arquivos no formato MIDI podem ser encontrados em diversos sites pela internet, uma sugestão é o [midiworld](http://www.midiworld.com/).

Então é isso, com o projeto montado e tudo configurado resta apenas apreciar as suas músicas favoritas tocadas por uma orquestra de drivers de disquete. =D
