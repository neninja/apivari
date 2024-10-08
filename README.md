# Apivari

Sistema que uso para gerenciar noites de jogos aqui em casa

## Desenvolvimento

### Ambiente

1. Duplique `.env.example` para `.env` e **mude o usuário (`DB_USERNAME`) e senha (`DB_PASSWORD`)**

```sh
cp .env.example .env
```

2. Baixe o Sail juntamente com as dependências do composer
```sh
docker run -v $(pwd):/var/www/html -w /var/www/html laravelsail/php82-composer:latest sh -c "composer config --global && composer install --ignore-platform-reqs"
```

```sh
sudo chown 1000:1000 -R vendor
sudo chmod 775 -R vendor
```

3. Suba o ambiente
```sh
./vendor/bin/sail up -d
```

> Esse comando é <a href="#Execução">utilizado sempre que quiser subir o ambiente ja configurado</a> também

4. Crie a `APP_KEY`
```sh
./vendor/bin/sail art key:generate
```

5. Crie as tabelas com alguns registros do *seeder*
```sh
./vendor/bin/sail art migrate:fresh --seed
```

6. Baixe as dependências javascript
```sh
./vendor/bin/sail npm i
```

### Execução local

> Precisa de 2 terminais abertos

1. Inicie o backend se necessário
```sh
./vendor/bin/sail up -d
```

> Interrompa com `./vendor/bin/sail down`

2. Execute o ambiente de frontend
```sh
./vendor/bin/sail npm start
```

> Interrompa com <kbd>ctrl</kbd><kbd>c</kbd>

Outros comandos úteis durante o desenvolvimento:

- `sail bash`
- `sail psql`
- `sail tinker`
- `sail art queue:work`
- `sail art optimize:clear`
- `sail composer i`

### Linting

```sh
./vendor/bin/sail php ./vendor/bin/pint
./vendor/bin/sail php ./vendor/bin/pint --dirty
```

### Testes

#### Ambiente

```sh
./vendor/bin/sail psql
create database apivari_testing;
```

#### Execução

```sh
./vendor/bin/sail test
./vendor/bin/sail test tests/Feature/BlablaTest.php
./vendor/bin/sail test --parallel --no-coverage
./vendor/bin/sail test --filter nomeDoTeste
```
