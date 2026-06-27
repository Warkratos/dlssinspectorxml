# Um pouco sobre Modelos de Apresentação (D3D11-12) com algumas dicas

O Modelo de Apresentação (Presentation Model) é o modo como o Windows exibe os frames de um jogo na tela. Ele pode ser inspecionado pelo painel de controle do Special K, pelo widget de framepacing, pela ferramenta PresentMon da Intel e mais recentemente, pelo FrameView da NVIDIA.
O objetivo é sempre alcançar o modelo com menor latência possível, que são **Hardware: Independent Flip** ou **Hardware Composed: Independent Flip** (quando MPO está ativo).

## Flip (D3D11/12)
<img width="3552" height="1338" alt="sankey_flip" src="https://github.com/user-attachments/assets/90e32ea4-78d3-4635-9b49-865bd87143fa" />
<sub>Fonte: https://wiki.special-k.info/Presentation_Model</sub><br/><br/>

Para jogos modernos no modelo Flip, o "Tela Cheia Exclusivo" no DirectX 12 é apenas emulado — o Windows muda resolução/taxa de atualização/espaço de cores temporariamente, mas funciona como uma janela sem bordas normal. No gráfico podemos ver que para atinger os modelos com menor latência, se usa das otimizações DirectFlip e Multi-Plane Overlay (MPO).
As otimizações DirectFlip no Windows 11, são feitas quando a chave "Otimizações para jogos em janela" está ativada no sistema.
<img width="958" height="301" alt="image" src="https://github.com/user-attachments/assets/0c1590b8-824a-4cdd-95e3-756514900acf" />
