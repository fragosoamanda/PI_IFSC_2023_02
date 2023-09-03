# Conceive
## _Lixeira Móvel com Wall-e_

![N|Solid](https://a.imagem.app/banBMY.png)

A internet das coisas (IOT) se refere à conexão e integração de equipamentos, aparelhos e tecnologias a internet, permitindo a comunicação e o gerenciamento deles. Com uma grande atenção voltada para esse setor, a IOT vem ganhando lugar em diversas áreas, incluindo a sustentabilidade. Há projetos relacionados a gerenciamento inteligente de energia, monitoramento de quantidade de lixo, consumo controlado de recursos (como água, por exemplo), entre outros.
Trazendo à tona a ideia de conectar aparelhos à internet e torná-los gerenciáveis, esse projeto visa algo semelhante, e com foco na sustentabilidade. O tema do projeto está relacionado com a disponibilização de uma lixeira para as pessoas descartarem lixo.
Enquanto pensávamos mais profundamente em uma proposta de projeto, encontramos uma carcaça de um robô no LPAE. Era uma versão do Wall-e (do filme “WALL-E”) impressa em uma impressora 3D (a base de plástico), como visto na figura 1. Ele já possuía os motores instalados (8 no total), mas não tinha nenhum circuito de alimentação ou que permitisse sua operação. A equipe decidiu implementar um projeto relacionado a esse robô.
Assim, a intenção desse projeto é conceber, desenvolver, implementar e operar um robô Wall-e teleoperado e no modo autônomo. Ele deve ser gerenciável remotamente, permitindo selecionar os modos de operação por meio de uma interface gráfica (aplicativo em Desktop).
No modo teleoperado, ele deve ser capaz de receber comandos do computador por meio da interface wireless. No modo autônomo, ele deve ser capaz de se mover por conta própria, evitando colisões por meio de técnicas de computação visual. Por exemplo, ao checar uma possibilidade de colisão, ele deve girar até que esteja em uma direção na qual possa se mover, e seguir seu trajeto.
Ele possuirá uma lixeira acoplada (de preferência na parte de trás dele para evitar que ela atrapalhe os demais mecanismos do robô), de forma a atuar como uma lixeira móvel automatizada. Com isso, traz à tona a ideia inicial da IOT (internet of things): conectar coisas (uma lixeira, nesse caso) à internet e torná-las gerenciáveis.

- #### Objetivos :
    - Interface com o usuário que permita:
    - Operar o Wall-e de forma teleoperada (comunicação Wifi)
    - Streaming de vídeo do Wall-e (por meio de Wifi)
    - Ligar/Desligar o modo autônomo
    - Desligar o Wall-e (executar um halt)
    - Controle dos motores
    - Tornar o Wall-e autônomo, evitando colisões ao se mover

- ##### Idéias de objetivos extras, caso sobre tempo para implementar:
    - Identificar lixo
    - Recolher lixo (precisa da instrução de alguém da área de mecânica ou um bom material de instrução)

- #### Lista dos principais materiais e ferramentas do projeto:
    - Carcaça do Wall-e impressa em 3D
    - Raspberry Pi 3B+
    - 8 Motores (2 de corrente contínua e 6 de passo)
    - Computador (para gerenciar o Wall-e)
    - Módulo de câmera do raspberry PI (talvez uma câmera USB funcione)


- #### Diagrama de blocos para implementação do projeto
![N|Solid](https://a.imagem.app/byI0xe.png)