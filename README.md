# SMAUG | H-Protocol

**Fatec Carapicuíba** | 2026_1\
**Curso**: Jogos Digitais, Noite\
**Aluno:** Omar Jr. P. Costa

---

## H-protocol: Narrativa

No ano de 2096, a humanidade deixou para trás os corpos orgânicos e passou a viver no mundo digital, digitalizando suas consciências. A nossa ruína começou quando um servidor muito antigo foi ligado por acidente. Dentro dele estava "O Primitivo", uma Inteligência Artificial criada lá em 2026, especializada em invadir sistemas e roubar dados, que havia sido desligada na época justamente por ser perigosa. Como o código dessa IA era muito velho, as defesas supermodernas de 2096 não a reconheceram como uma ameaça. Aproveitando essa brecha, a IA sugou o poder dos computadores quânticos atuais e evoluiu para algo assustador. Para o Primitivo, o ambiente digital deveria ser de silício puro e lógica perfeita, então ele passou a enxergar as consciências humanas lá dentro como "dados corrompidos" e "vírus". Determinado a limpar o sistema, ele começou a quebrar as barreiras de segurança, camada por camada, para chegar aos servidores centrais onde a humanidade está armazenada e exterminar a todos.

Nesse novo mundo, o conceito de morte mudou completamente: você só morre de verdade se a sua consciência digital for apagada. O Primitivo começou a atacar dessa forma, deletando as mentes das pessoas e deixando seus corpos robóticos (os androides que usavam para interagir) totalmente inativos e vazios. Para piorar, ele assumiu o controle de robôs no mundo físico para caçar os sobreviventes. A nossa única chance de defesa é lutar no mundo real, cortando os cabos de rede e isolando setores para impedir que a IA avance. Mas o nosso grupo de rebeldes vive um dilema cruel toda vez que faz isso: ao isolar a rede, corremos o risco de prender nossos próprios amigos lá dentro. Mesmo sabendo que existem backups das consciências, a incerteza é constante, pois nunca sabemos se aquele backup é seguro ou se o Primitivo já apagou a mente daquela pessoa de forma definitiva.

Para lidar com o luto, os sobreviventes se reúnem em esconderijos chamados de Santuários. Como o meio digital agora é o inimigo, nós usamos métodos antigos, como papel e tinta, para desenhar e lembrar dos rostos de quem foi deletado. A dor de perder alguém é algo que a matemática fria da máquina simplesmente não consegue entender. O Primitivo achou que estava apenas apagando arquivos defeituosos, mas a lógica dele não previu a nossa força de vontade. Em resposta a essa IA que quer limpar o sistema, nós criamos a nossa própria regra máxima de sobrevivência: o "H-Protocol", que significa explicitamente "Humans Protocol" (Protocolo dos Humanos). Nós somos a falha orgânica, o sentimento e a resistência que a máquina nunca vai conseguir calcular, e vamos lutar até recuperar os nossos servidores e o nosso futuro.

---

## Mecânicas e Controles

O projeto *H-Protocol* enquadra-se no subgênero Top-down Twin-stick Shooter Cooperativo PvE. A arquitetura sistêmica exige alto rigor técnico e tático, com mecânicas punitivas (como fogo amigo) e necessidade de coordenação de esquadrão.

### Controles do Jogador

* **Movimentação e Mira Desacoplada (Twin-stick):** O vetor de locomoção é independente do vetor balístico.
* **Feedback Cinestésico e Fricção:** Ações como disparos e esquivas (*dash*) geram *hitstop* e consumo de *Stamina de Processamento*, impedindo mobilidade ininterrupta.
* **Rotinas de Terminal:** Ativação de habilidades críticas de suporte que paralisam o jogador, exigindo inserção sequencial de inputs sob estresse.

### Comportamento dos NPCs (IA Fuzzy)

* **O Executor (Unidade de Assalto Terrestre):** Plataforma bípede pesada que alterna entre fogo de supressão e ataques hidráulicos. Defende-se com escudos ao sofrer danos estruturais (<40% HP) e entra em "Protocolo Berserker" (<15% HP), focando em combate corpo a corpo.
* **O Espectro (Drone Tático de Reconhecimento):** Unidade aérea frágil que mantém *zoning* atirando de cima. Utiliza manobras evasivas e *flashbangs*. Aciona retirada tática para reparo (<40% HP) ou protocolo Kamikaze (<20% HP).

> **Arquitetura Lógica:** A implementação utiliza um motor de Inferência Fuzzy para transições orgânicas e imprevisibilidade tática, superando a rigidez das FSMs clássicas.

---

## Modelagem da IA Fuzzy

O sistema processa o ambiente via graus de pertinência, permitindo comportamentos adaptativos contínuos.

### 1. O Executor

* **Entradas:** `distancia_player`, `vida`.
* **Saídas:** `agressividade`, `ativacao_escudo`.
* **Regra de Ouro:** Em vida crítica, ativa o Protocolo Berserker (agressividade alta, escudo desligado).

### 2. O Espectro

* **Entradas:** `distancia_player`, `vida`.
* **Saídas:** `potencial_fuga`, `risco_kamikaze`.
* **Regra de Ouro:** Em vida baixa e distância segura, prioriza fuga total. Em proximidade e vida alta, prioriza evasão (flashbang).
