# Global Streamline DLLs Override

Essa ferramenta faz a substituição das DLLs do Frame Generation, Super Resolution e Ray Reconstruction de forma global no sistema, e não só isso, ela também atualiza as DLLs Streamline (quando suportado pelo jogo) que incluem: NVIDIA Reflex, Multi-Frame-Generation. Com isso, é possivel usar MFG em jogos que até não tinham suporte a ele, mas tinha o Frame Generation 1X.


Roda de forma portátil, ou seja, não requer instalação, ela substitui as DLLs na pasta ProgramData\NVIDIA\NGX, fazendo o driver carregar elas nos jogos.

## Como usar

Baixe a última versão dessa ferramenta (nvidiaDlssGlom.exe) no repositório do desenvolvedor -> https://github.com/SimonMacer/AnWave/releases/tag/AnWave-DLSS


![Screenshot](https://i.imgur.com/qSoSCey.png)

Marque a caixa **"Enable NVIDIA Streamline Override Mode"**

A caixa **"Force Enable DLSS Override on All DLSS Titles"** serve para que você controle o override pelo NVIDIA Profile Inspector, com ela **MARCADA**, todos os jogos terão suas DLLs substituidas pela última, com ela **DESMARCADA**, você controla quando substituir a DLL pelo Profile Inspector.

A caixa **"Show DLSS Indicator"** ativa o overlay do DLSS no jogo, alterando o registro (o mesmo que faz o DLSS Overlay Toggle)

Minha recomendação é deixar igual ao da screenshot acima, apenas desmarcar o Show DLSS Indicator depois que confirmar que funcionou.

Clique em **"Download from server"** e pronto.

**Para desfazer tudo e voltar ao normal, vá até a pasta ProgramData (Windows + R, %ProgramData%), encontre a pasta NVIDIA e apague a pasta NGX.**
