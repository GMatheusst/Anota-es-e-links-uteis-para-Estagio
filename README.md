
[anotações Uteis para Git](https://github.com/user-attachments/files/16337722/anotacoesGit.txt)

[Laravel](https://laravel.com/)

[Composer](https://getcomposer.org/)

[Laravel Estudo](https://github.com/user-attachments/files/16338710/laravelEstudo.txt)

[Laravel explicações](https://www.devmedia.com.br/guia/laravel/38191)

[Intruções BackEnd](https://github.com/user-attachments/files/16338784/intrucoes.txt)

[Intruções FrontEnd](https://github.com/user-attachments/files/16338824/intrucoesFrontEnd.txt)

[Emojis commits](https://github.com/user-attachments/files/16351484/035de27d6ed1dce0b36a-0120078468630c2a0566357f1d04067626d80a29.zip)

[Laravel 1(explicação Superficial)](https://github.com/user-attachments/files/16353622/laravel.txt)

[Laravel 1.1(explicação Completa)](https://github.com/user-attachments/files/16353628/laravel1.1.txt)

[Laravel 1.2(implementação)](https://github.com/user-attachments/files/16353631/laravel1.2.txt)

[Descrição do projeto](https://github.com/user-attachments/files/16417984/Documentacao.do.projeto.-.EmailVerficationCode.txt)

[Codigo de Verificação de Email](https://github.com/user-attachments/files/16418360/codigo.txt)

[Task Scheduling](https://dev.to/n3rdnerd/laravel-task-scheduling-scheduling-artisan-commands-3311)

[Task code](https://github.com/user-attachments/files/16432301/taskinfo.txt)

[Task Scheduling 2](https://www.golinuxcloud.com/set-cron-in-laravel/)

Ainda não é possível fazer o merge das alterações pelos seguintes motivos:

No método store(), linha 19, a validação de email tem que verificar se o usuário com esse email existe no banco, exists:users,email

A validação do método reset(), linha 50, requer um email, porém, somente o token é suficiente para verificar se a redefinição pode ser feita.

Dentro da condição do método reset(), a parte Hash::check(...) na linha 63, precisa ser antecedida por uma !, pois a condição verifica se o token é inválido.

A migration 2024_08_01_174658_add_id_to_password_reset_tokens_table.php e 2024_08_01_175045_add_email_to_password_reset_tokens_table.php não são necessárias, e resultam em erros, pois essa tabela já possui uma primary key, que é a coluna de emails. Você pode explicitar no model qual é a primary key da tabela com public $primaryKey = 'email';

Na verificação de RateLimit, na linha 27, o número de mínimo de tentativas tem que ser 1, pois dessa forma na segunda request usuário já recebe o aviso, e pode enviar outro email apenas após 60 segundos. Além disso, na response retornada quando RateLimiter::tooManyAttempts for verdadeiro deve ser o tempo para a próxima request ser liberada.

Nas response do método reset(), retire o conteúdo 'teste*'.

No método reset(), linha 70, a verificação se o usuário existe não é necessária, pois deveria ser feita antes de criar o token.
