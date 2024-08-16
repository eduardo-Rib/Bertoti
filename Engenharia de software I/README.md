Atividade 1
We see three critical differences between programming and software engineering: time, scale, and the trade-offs at play. On a software engineering project, engineers need to be more concerned with the passage of time and the eventual need for change. In a software engineering organization, we need to be more concerned about scale and efficiency, both for the software we produce as well as for the organization that is producing it. Finally, as software engineers, we are asked to make more complex decisions with higher-stakes outcomes, often based on imprecise estimates of time and growth.

Na engenharia de software há mais preocupações do que apenas programar, é necessário de preocupar com o gerenciamento de tempo, o quão escalavel e eficiente o programa é, etc. O engenheiro de sofware tem que se preocupar com possiveis mudanças ao longo do processo e tomar decisões delicadas rapidamente que não comprometam o desenvolvimento.




Atividade 2
3 exemplos de trade-offs levando em consideração requisitos nao funcionais:

1. Desempenho vs. Escalabilidade
Técnicas de otimização mais agressivas e complexas podem funcionar bem em uma escala menor, mas podem ser difíceis de ajustar quando o sistema precisa escalar para suportar um número muito maior de usuários

2. Segurança vs. Usabilidade
Adicionar várias etapas de validação, criptografia de dados etc, aumentam a segurança, mas pioram a usabilidae do sistema, tornando complexo a utilização do sistema pelo usuário 

3. Custo de Desenvolvimento vs. Manutenibilidade
Optar por uma solução mais barata e rápida para desenvolvimento, mas essas soluções podem resultar em código menos organizado e menos documentado, o que pode dificultar a manutenção e a evolução futura do sistema




Atividade 3
![image](https://github.com/user-attachments/assets/4efee842-3075-480d-a657-190d03858a6e)


1º Exemplo de trade-off
 
O Federated Strato Column é um componente do sistema backend do Twitter, responsável por gerenciar e fornecer dados estruturados e desestruturados, como tweets, informações de usuários, e outros conteúdos necessários para compor a experiência do usuário na plataforma.

O termo "federated" implica que essa estrutura é distribuída e integrada a vários sistemas, possibilitando o acesso a diferentes fontes de dados em vários servidores ou locais, assegurando que o Twitter consiga escalar o fornecimento de conteúdo para milhões de usuários simultaneamente.

Por exemplo, ao carregar um tweet na timeline, o Federated Strato Column busca os detalhes do tweet, como texto, mídia associada, informações do autor, e interações (curtidas, retweets, etc.).

O Federated Strato Column determina quais conteúdos são visíveis para o usuário com base em regras de segurança, moderação, ou preferências pessoais. Isso pode incluir a remoção de tweets que violem as diretrizes da plataforma ou que sejam considerados irrelevantes para o usuário específico.

O Federated Strato Column é capaz de melhorar a escalabilidade do Twitter, envolvendo processos complexos de consultas em várias bases de dados, a fim de filtrar os conteúros de forma que sejam exibidos apenas os melhores conteúdos para determinado tipo usuário, desta froma, aumentanto a retenção de usuários. Entretanto, isso aumenta muito a complexidade e custo do sistema para simplesmente carregar uma tela inicial.

Por isso, é evidente que, entre uma melhor escalabilidade ou um menor custo de desenvolvimento, foi preferido uma melhor escalabilidade, haja vista que uma rede social desse porte necessita atender uma demanda enorme de requisições e ser capaz de manter os usuários o máximo de tempo online na plataforma.




2º Exemplo de trade-off

A TLS-API é uma interface que facilita a comunicação segura entre diferentes componentes de um sistema, usando o protocolo TLS. 

No contextp do twitter, a TLS-API era usada para permitir que os diferentes componentes do Twitter, como o frontend e o backend, se comunicassem de maneira segura, especialmente ao lidar com dados sensíveis, como informações de usuários e autenticações.

De acordo com a imagem, o Twitter estava em processo de substituí-la por uma tecnologia ou abordagem mais moderna e eficiente. Isso geralmente ocorre quando uma tecnologia se torna obsoleta, seja por razões de segurança, desempenho ou manutenção, e a empresa migra para alternativas melhores.

Portanto, entre segurança e Custo de Desenvolvimento, foi optado por parar de utilizar a TLS-API, por ja ser um protocolo de segurança desatualizado, que não tem o mesmo nivel relação a outros protocolos mais modernos.  
