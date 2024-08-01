
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

[Httpie](https://httpie.io/app)

[Mailtrap](https://mailtrap.io/inboxes/3049831/messages/4372095646/advanced_html_analysis)

Ainda não é possível fazer o merge das alterações pelos seguintes motivos:

A validação do método reset(), linha 50, requer um email, porém, somente o token é suficiente para verificar se a redefinição pode ser feita.

Dentro da condição do método reset(), a parte Hash::check(...) na linha 63, precisa ser antecedida por uma !, pois a condição verifica se o token é inválido.

Na verificação de RateLimit, na linha 27, o número de mínimo de tentativas tem que ser 1, pois dessa forma na segunda request usuário já recebe o aviso, e pode enviar outro email apenas após 60 segundos. Além disso, na response retornada quando RateLimiter::tooManyAttempts for verdadeiro deve ser o tempo para a próxima request ser liberada.



<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    /**
     * Run the migrations.
     */
    public function up(): void
    {
        Schema::create('users', function (Blueprint $table) {
            $table->id();

            $table->string('pipefy_id')->unique()->nullable();

            $table->string('name');
            $table->string('cpf', 11)->unique()->nullable();

            $table->string('email')->unique();
            $table->string('phone', 11)->unique()->nullable();

            $table->timestamp('email_verified_at')->nullable();

            $table->tinyInteger('access_level')->default(0);

            $table->string('password')->nullable();
            $table->rememberToken();

            $table->timestamps();
            $table->softDeletes();
        });

        Schema::create('password_reset_tokens', function (Blueprint $table) {
            $table->id()->primary();
            $table->string('email');
            $table->string('token');
            $table->timestamp('created_at')->nullable();
        });

        Schema::create('sessions', function (Blueprint $table) {
            $table->string('id')->primary();
            $table->foreignId('user_id')->nullable()->index();
            $table->string('ip_address', 45)->nullable();
            $table->text('user_agent')->nullable();
            $table->longText('payload');
            $table->integer('last_activity')->index();
        });
    }

    /**
     * Reverse the migrations.
     */
    public function down(): void
    {
        Schema::dropIfExists('users');
        Schema::dropIfExists('password_reset_tokens');
        Schema::dropIfExists('sessions');
    }
};
