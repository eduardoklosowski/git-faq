Versionar Diretório
===================

Problema
--------

O projeto necessita de um diretório, por exemplo, para guardar arquivos que foram enviados pelos clientes ou armazenar logs, sendo que esses arquivos devem ser ignorados pelo git (não devem ser versionados), por não fazerem parte do código. Porém ao criar uma regra no ``.gitignore`` e clonar o repositório em outro local ou computador, este diretório não é criado.


Solução
-------

Uma opção simples seria criar a regra no ``.gitignore`` e fazer a aplicação tentar criar o diretório caso ele não exista, o que já funcionaria. Porém seria necessário executar a aplicação para que ela crie os diretórios necessários, podendo gerar uma confusão já que esses diretórios não existiriam para alguém que verificou o repositório previamente, como se eles aparecessem magicamente.

Infelizmente o git não versiona diretórios isoladamente, todo diretório deve conter pelo menos um arquivo dentro dele, ou de um subdiretório seu, para ser versionado pelo git e aparecer no repositório. Por este motivo muitos criam um arquivo chamado ``.gitkeep`` dentro desses diretórios, porém poderia ser qualquer outro nome, esse é apenas o mais usado nos exemplos (existem projetos que nomeiam esses arquivos como ``delete.me`` ou semelhante). Esse arquivo pode estar em branco ou ter algum conteúdo, não faz diferença para essa abordagem.

Porém para a correta configuração do repositório, este arquivo deve ser versionado, enquanto os demais arquivos do diretório não, isso pode ser feito com regras no ``.gitignore``, como no exemplo a baixo, onde apenas o arquivo ``.gitkeep`` será versionado dentro do diretório ``logs``:

.. code-block:: text
  :linenos:

  logs/*
  !logs/.gitkeep

Outra opção seria criar um arquivo ``.gitignore`` dentro do diretório:

.. code-block:: text
  :linenos:

  *
  !.gitignore


Troubleshoot
------------

Caso o diretório não apareça como alterado ao executar um ``git status``, primeiramente verifique se não existe nenhuma regra que ignora o diretório onde o arquivo ``.gitkeep`` está, caso exista, altere a regra para ignorar apenas o que está a baixo dele, adicionado um ``/*`` no final.


Links Externos
--------------

- `Manpage: gitignore <https://git-scm.com/docs/gitignore>`_
