## Sobreposição de DLSS pelo Profile Inspector
As funcionalidades adicionadas ao NVIDIA App podem ser forçadas em qualquer jogo e até mesmo de forma global pelo Inspector usando esse XML, abaixo uma breve explicação de cada item da seção "DLSS Overrides".

**NOTA:** SR = Super Resolution | RR = Ray Reconstruction | FG = Frame Generation

**DLSS-FG - Multi-Frame-Generation Count** -> Especifica em quantas vezes serão gerados os quadros do Frame Generation

**DLSS-FG, DLSS-RR e DLSS - DLL Override** -> ON = Faz com que o driver substituia a DLL do DLSS do jogo com a dele, OFF = Padrão

**DLSS-FG, DLSS-RR e DLSS - Force Preset Letter** -> Aqui é possível forçar algum preset de cada parte do DLSS, recomendo usar a opção "Latest Preset" em todos

**DLSS-RR e DLSS - Forced Quality Level** -> Possibilita forçar e fixar os modos do Ray Reconstruction e Super Resolution, mesmo que o jogo não suporte.

**DLSS e DLSS-RR - Forced Scaling Ratio** -> Customiza a porcentagem de escalonamento do DLSS. Para ativar a funcionalidade, coloque o Force Profile Mode em Custom e escolha a opção do Scaling Factor que deseja.

## Sobreposição Global de DLSS através do driver em qualquer jogo
![image](https://i.imgur.com/qSoSCey.png)

Veja como fazer [aqui](https://github.com/renannmp/dlssinspectorxml/blob/main/globaloverride.md)
