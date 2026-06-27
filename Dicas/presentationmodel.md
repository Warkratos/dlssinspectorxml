# Modelos de Apresentação

O Modelo de Apresentação (Presentation Model) é o modo como o Windows exibe os frames de um jogo na tela. Ele pode ser inspecionado pelo painel de controle do Special K, pelo widget de framepacing, pela ferramenta PresentMon da Intel e mais recentemente, pelo FrameView da NVIDIA.
Antes de mostrar os modelos de apresentação, precisamos saber que os jogos podem usar 2 métodos de swap effect, são chamados de **BitBlt** e **Flip**, sendo o último o mais moderno e o que tem menor latência.
<br/><br/>
**BitBlt**: o frame é copiado para a composição do desktop; é o modelo legado e tende a ser menos eficiente.  
**Flip model**: o buffer do jogo é “trocado” de forma mais direta com a pipeline de exibição, reduzindo cópias desnecessárias e podendo baixar a latência.
<br/>
Com esses 2 Swap Effects, temos os modelos de apresentação, a tabela abaixo explica cada um deles.
<br/><br/>
<img width="990" height="146" alt="image" src="https://github.com/user-attachments/assets/70e1f157-3211-4e86-91bf-14f4b0a73a1d" />  
O objetivo é sempre alcançar o modelo com menor latência possível, que são **Hardware: Independent Flip** ou **Hardware Composed: Independent Flip** (quando MPO está ativo), pois até mesmo a NVIDIA já explicou que o VSYNC + Frame Generation por exemplo, precisa do Independent Flip para obter a menor latência de jogo. 
<br/><br/>
<img width="1660" height="330" alt="HLhJc10asAAcZW4" src="https://github.com/user-attachments/assets/19039663-cca4-4a8f-8fb6-b4ee221ee722" />
<br/><br/>
Descubra quais fatores influenciam a ativação desses modelos, a seguir.
<br/><br/>
## Flip (D3D11/12)
<img width="3552" height="1338" alt="sankey_flip" src="https://github.com/user-attachments/assets/90e32ea4-78d3-4635-9b49-865bd87143fa" />
<sub>Fonte: https://wiki.special-k.info/Presentation_Model</sub><br/><br/>

No gráfico podemos ver que para atingir os modelos com menor latência, se usa das otimizações DirectFlip, Otimizações de Tela-Cheia e Multi-Plane Overlay (MPO). Além disso no gráfico acima, a seção "Exclusive Fullscreen (FSE)" não se aplica a jogos DirectX 12 pois o **"Tela Cheia Exclusivo" no DirectX 12** é apenas emulado — o Windows muda resolução/taxa de atualização/espaço de cores temporariamente, mas funciona como uma janela sem bordas normal.
<br/><br/>

## BitBlt (D3D11)
<img width="3552" height="1515" alt="sankey_bitblt" src="https://github.com/user-attachments/assets/519c42e0-17b6-4e1c-b335-d17fbe1a858d" />
<sub>Fonte: https://wiki.special-k.info/Presentation_Model</sub><br/><br/>

Já para jogos que utilizam do swap effect BitBlt, as otimizações DirectFlip podem fazer bem mais melhorias, quando usado em janela sem borda ou janela. Pois a partir da versão 22H2 do Windows 11, ele promove esses jogos para o modelo Flip!

### DirectFlip Optimizations
As otimizações DirectFlip no Windows 11 (desde a versão 22H2), são feitas quando a chave **"Otimizações para jogos em janela"** está ativada no sistema, que [promove jogos DirecX 10 e 11 do modelo BitBlt para Flip no modo janela sem borda e janela](https://support.microsoft.com/pt-BR/Windows/Hardware/Display-Graphics/optimizations-for-windowed-games-in-windows-11), e adiciona junto, suporte a VRR e AutoHDR no jogo, quando compatível.
<br/><br/>
<img width="958" height="301" alt="image" src="https://github.com/user-attachments/assets/0c1590b8-824a-4cdd-95e3-756514900acf" />
<br/><br/>
Em versões anteriores ao 22H2 do Windows 11 ou até mesmo no Windows 10, para fazer essa promoção automática, pode ser usado a [ferramenta Special K](https://wiki.special-k.info/), não recomendada para jogos online.

### Multi-Plane Overlay (MPO)
Com MPO ativo, o Windows pode manter o jogo em Hardware Composed: Independent Flip e colocar um overlay desenhado por cima do jogo — Discord, Xbox Game Bar, NVIDIA overlay, notificação do sistema, captura, etc. —  em outro plano de hardware, sem derrubar o caminho principal do jogo. Ssem MPO a chance de cair de Independent Flip aumenta bastante, ainda mais com o uso de overlays, o que aumenta a latência.  

### Como inspecionar o modo de apresentação
Com o [PresentMon](https://game.intel.com/us/intel-presentmon/) (ou com o RTSS usando o sensor do presentmon), coloque o Preset em "Custom" e clique no botão "Edit" > "Add New Widget" > "Present Mode"
<br/><br/>
<img width="392" height="267" alt="image" src="https://github.com/user-attachments/assets/156d52c5-21d2-4168-952e-e7e4c5a3930d" />
<br/>
A informação "Present Mode" vai aparecer informando o modelo da janela do jogo.


# Considerações
O jogo pode ficar em "Hardware: Independent Flip" sem o MPO, porém ao usar overlays, o jogo pode despencar para o modo com mais latência, e o MPO ainda se quebra com algumas limitações técnicas, a minha recomendação é sempre deixar o MPO ligado (se for desligar o MPO, inspecione se o jogo está no modelo Independent Flip, não use Overlays do Discord, etc), para que tenha muito mais chances da janela ser feita na composição "Hardware Composed: Independent Flip" e "Otimizações para jogos em janela" **SEMPRE** ativado.<br/>
Como regra geral:<br/>
**DX12** → sempre usa Flip model, mas pode usar modo de apresentação Composed Flip (Alta Latência) se as otimizações de DirectFlip estiverem desativadas e MPO quebrado.<br/>
**DX11/10 em janela sem bordas, sem overlay** → provavelmente Flip, se as condições de DirectFlip e MPO estiverem ativadas (Windows 11 22H2+), no modo "Tela Cheia" ele usará o modo Flip correto se "otimizações para jogos em janela" estiver ativado.<br/>
**DX11/10 com overlay de terceiros (NVIDIA App, Discord, etc.)** → pode cair para BitBlt/Composed com otimizações de janela desativados e/ou MPO<br/>
**Jogos mais antigos (DX9, OpenGL)** → quase sempre BitBlt
<br/><br/><br/><br/><br/>
Fonte Principal: [Special-K](https://www.special-k.info/)
