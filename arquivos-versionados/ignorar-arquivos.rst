Ignorar Arquivos
================

Problema
--------

Podem existir alguns arquivos que ficam dentro do diretório do repositório git, como:

- Arquivos de configuração, que podem conter dados sensíveis como senhas.
- Arquivos compilados, que podem ser gerados automaticamente ao recompilar o projeto.
- Bibliotecas externas, que podem ser baixadas novamente, além de provavelmente serem versionadas externamente.

Desta forma esses arquivos não devem ser compartilhados no repositório git, tanto por questões de segurança (evitando publicar as senhas), otimização do repositório (evitar o aumento do seu tamanho) e redução de conflitos (a compilação tende a gerar arquivos diferentes cada vez que executada, como a inclusão da data de compilação).


Solução
-------

Esses arquivos devem ser ignorados pelo git, de forma que eles não sejam versionados, mesmo que existam dentro do diretório do repositório git.

Esta configuração pode ocorrer em três lugares:

- Arquivo ``.gitignore`` dentro do repositório, que aplica as regras para o diretório atual e a todos a baixo dele.
- Arquivo ``.git/info/exclude``, que aplica as regras para todo o repositório.
- Arquivo ``~/.config/git/ignore``, que aplica as regras para todos os repositórios acessados pelo usuário.

O melhor lugar depende de cada caso. A opção mais adotada é um arquivo ``.gitignore`` na raiz do projeto, que é versionado pelo git, desta forma essas regras serão compartilhadas por todos que usam o repositório, além de ficarem centralizadas. Em casos onde existam muitas regras, regras mais específicas para diretórios, elas podem ser divididas em outros ``.gitignore``, podendo existir mais de um ``.gitignore`` em diferentes diretórios no mesmo repositório.

Porém em casos onde um programador usa um IDE específica que cria arquivos de configuração dentro do diretório do projeto, e se essas regras não forem aceitas por quem controla o repositório, elas podem ser feitas no arquivo ``.git/info/exclude`` para o projeto específico, ou mesmo em ``~/.config/git/ignore`` para ser aplicada a todos os repositórios. Mas essas regras não serão compartilhadas com as demais cópias deste repositório, devendo ser refeitas.


Troubleshoot
------------

Caso as regras não estejam sendo aplicadas, como um arquivo continuar aparecendo no comando ``git status``, verifique:

- Se o nome do arquivo de configuração está correto.
- Se as regras estão usando a barra normal (``/``) e não barras invertidas (``\``).
- Vá no diretório onde encontra-se o ``.gitignore`` ou na raiz do repositório e tente listar o arquivo com o comando ``ls``, por exemplo, após isso verifique se a regra está de acordo.
- Verifique se o arquivo já não estava sendo versionado antes da criação da regra.


Links Externos
--------------

- `Manpage: gitignore <https://git-scm.com/docs/gitignore>`_
