---
layout: post
title:  "Sobre este blog"
excerpt: "Este é um post detalhando o processo de construção deste blog, desde qual a tecnologia CMS até qual o sistema de deploy utilizado"

---


Apresento a vocês o meu ["novo blog"][1], ou melhor, reformulado, porque o registro existe desde 2009, mas, eu nunca tratei da forma que deveria e todos os anos a minha meta  era "começar a escrever" e compartilhar o meu conhecimento de alguma forma. Não preciso nem dizer que todos os finais dos anos, essa meta não era alcançada e eu me sentia muito mal com isso, por incrível que pareça este ano eu não coloquei na meta e já comecei com força total!!!
Você vai encontrar alguns registros meus no histórico do WayBackMachine, mas decidi apagar tudo, e iniciar tudo novamente.

## Qual foi a plataforma utilizada e porque escolhi

No passado, eu utilizei o Wordpress mas não obtive sucesso, principalmente porque eu precisava pagar mensalmente um serviço de hospedagem e isso me desmotivou muito. Vejam bem, não estou dizendo que a plataforma é ruim, pelo contrário, Wordpress é sensacional, acredito que é a principal plataforma de CMS, com uma comunidade sensacional, já me salvou de diversas "enrascadas" e até hoje eu recomendo para diversos clientes, principalmente porque você não precisa conhecer tecnicamente, a administração é intuitiva e com a quantidade de plugins e temas (pagos ou grátis) existentes, você praticamente não precisa se preocupar em desenvolver algo novo. Sendo assim, não considerei o Wordpress como uma alternativa.  
Encontrei diversas plataformas sensacionais, como o próprio ["Medium"][3], que tem uma base de leitores/usuários muito grande, encontrei também o ["Ghost"][4], que eu testei e achei muito útil e simples de escrever. Fiz os testes com o ["MiniBlog"][5], e achei sensacional, é uma arquitetura simples para entender, principalmente porque já conheço C#. Infelizmente todos os casos anteriores eu precisaria pagar a hospedagem (sendo cloud ou não), e eu não quero ter este compromisso neste momento.  
Continuei a minha pesquisa e encontrei os ["blogs estáticos"][6], a primeira plataforma que eu testei e eu gostei MUITO foi o ["Hugo"][2], construído em Go, e a minha primeira atividade foi construir o tema para o blog e para isso utilizei alguns blogs que acho incríveis como "guia", sendo eles o do ["Willian Justen"][8], ["Jessie Frazelle"][9], ["Phil Haack"][10] e o ["Jeff Atwood"][11]. Sou horrível para escolher cores e as fontes para o texto, e posso te dizer que estes blogs me ajudaram muito com isso.   
O primeiro grande desafio era entender como construir o tema e conforme fui avançando na construção, encontrei algumas dificuldades, até que uma em especifico me TRAVOU completamente e eu acho SUPER importante ter disponível no meu blog, são os comentários, por padrão o Hugo permite utilizar o Disqus, e eu não quero nenhuma plataforma "freemium", principalmente porque não quero que você tenha o constrangimento de abrir propagandas impróprias e principalmente que eu não tenha controle sobre o que estão inserindo no HTML/JS do meu site, por outro lado não quero pagar por um serviço que em momento nenhum deve gerar receita, encontrei ["alguns comentários"][14] de pessoas utilizando o Kaiju, mas novamente, precisaria de um server para isso, e as ["outras propostas oferecidas para sistema de comentário"][15] seria utilizando serviços de terceiros, sendo assim abandonei o Hugo e vi que não ofereceriam um suporte tão rápido para arquivos estáticos que outras plataformas estavam aceitando. 
A próxima plataforma que encontrei foi o ["Jekyll"][7] (nome derivado de uma série de livros "The strange case of Dr. Jekyll and Mr. Hyde"), plataforma construída em Ruby, e uma das mais utilizadas como blog estático, antes de migrar o tema que eu já havia construído, procurei pelas formas de comentários dentro da plataforma, e encontrei ["um post do Phill"][12] e achei SENSACIONAL a maneira que foi desenvolvida, resolvi testar, fiz alguns ajustes, um pull request para adicionar a análise de sentimento no comentário que está inserindo (eu já sei logo de cara se você está sendo grosso ou não comigo hehehe) e funcionou perfeitamente.  
Para resumir a questão do comentário: você ao escrever o comentário, enviará um POST para uma Azure Function, ela faz toda a composição do Pull request, criando o arquivo YML, criando a mensagem do Pull request, realiza automaticamente uma chamada no Cognitive Services do Azure, para descobrir se é um comentário positivo ou negativo, e utilizando o pacote do OctoKit é enviado o Pull request no repositório do blog, pretendo escrever um pouco melhor sobre isso mais para frente, enquanto isso vocês conseguem ver ["o post do Damien"][13]. 

## Avaliar os comentários

Como um comentário nada mais é do que um pull request no repositório do blog, eu primeiramente vejo o score que o ACS reconheceu para o texto, e posteriormente faço a leitura do comentário em si, se existir algum conteúdo impróprio ou inadequado, eu simplesmente rejeito o pull request e nada acontece, caso contrário, eu aceito o pull request, e o processo de deploy automaticamente reconhece um commit novo na master e libera o comentário no site.

## Onde estou hospedando

Para hospedagem eu inicialmente havia configurado o próprio GitHub pages, ele oferece suporte a custom domain, TLS/SSL e suporte ao Jekyll, porém, eu encontrei a Netlify, que além de me oferecer todos os recursos anteriores, também disponibiliza muitos builds por minuto, e eu achei a plataforma transparente relacionado aos builds que realiza, estou muito contente com o resultado que eles estão entregando, sendo que, a cada novo build enviam um e-mail automaticamente, se algum build quebrou, eles não publicam o site e notificam que o build quebrou, e eu também posso configurar outros ambientes, muito parecido ao ciclo de CI/CD (este particularmente eu não estou utilizando). 

## Conclusão

A construção do blog não foi fácil, principalmente porque eu busquei construir praticamente tudo do zero e fazendo por si só, mas posso dizer que o resultado foi surpreendente e eu gostei muito de como está construído.  
Se ficaram com alguma dúvida ou com algo que eu poderia adicionar no texto, entrem em contato comigo pelos comentários :heartpulse:





[1]: https://web.archive.org/web/*/http://nicolastarzia.com/
[2]: https://gohugo.io/
[3]: https://medium.com/
[4]: https://ghost.org/
[5]: https://github.com/madskristensen/MiniBlog/
[6]: https://www.staticgen.com/
[7]: https://jekyllrb.com/
[8]: https://willianjusten.com.br/
[9]: https://blog.jessfraz.com/
[10]: https://haacked.com/
[11]: https://blog.codinghorror.com/
[12]: https://haacked.com/archive/2018/06/24/comments-for-jekyll-blogs/
[13]: https://damieng.com/blog/2018/05/28/wordpress-to-jekyll-comments
[14]: https://discourse.gohugo.io/t/static-comment-for-hugo/1944
[15]: https://gohugo.io/content-management/comments/