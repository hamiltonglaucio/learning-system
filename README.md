# Learning System

Sistema educacional para aprendizado de línguas estrangeiras, com arquitetura baseada em PHP 8.4, Docker e ferramentas de análise estática, voltado para desenvolvimento profissional de alta qualidade e segurança.

---

## 🧱 Estrutura do Projeto

```
learning-system/
├── .docker/
│   ├── nginx/
│   │   └── nginx.conf
│   └── php/
│       ├── conf.d/
│       ├── Dockerfile
│       ├── composer.json
│       ├── php.ini
│       ├── xdebug.ini
│       ├── phpcs.xml
│       ├── phpstan.neon
│       ├── .php-cs-fixer.php
│       └── phpunit.xml.dist
├── public/
│   └── index.php
├── src/
├── tests/
└── docker-compose.yml
```

---

## ⚙️ Requisitos

- **Docker** e **Docker Compose** instalados
- Nenhuma instalação de PHP ou Composer localmente
- Apenas o Docker lida com tudo

---

## ▶️ Subindo o ambiente

```bash
docker compose up -d --build
```

---

## 📦 Instalação das dependências

Após os containers estarem de pé, acesse o container PHP:

```bash
docker exec -it php bash
```

E execute:

```bash
composer install
```

---

## 🧪 Executando os testes

### PHPUnit:

```bash
XDEBUG_MODE=coverage php vendor/bin/phpunit --configuration=.docker/php/phpunit.xml.dist
```

---

## 🔍 Ferramentas de Qualidade e Análise Estática

### PHPStan:

```bash
XDEBUG_MODE=off php vendor/bin/phpstan analyse
```

### PHP_CodeSniffer (PSR2 + Regras de Segurança):

```bash
php vendor/bin/phpcs --standard=.docker/php/phpcs.xml src/
```

### PHP CS Fixer:

```bash
php vendor/bin/php-cs-fixer fix --config=.docker/php/.php-cs-fixer.php
```

Ou, durante edição automática via File Watcher no PHPStorm.

### PHPMD:

```bash
php vendor/bin/phpmd src/ text cleancode,codesize,controversial,design,naming,unusedcode
```

---

## 🐞 Debug com Xdebug

- Xdebug instalado e ativado via Docker com suporte ao PHPStorm
- Arquivo `xdebug.ini` configurado em `.docker/php/conf.d/`
- Debug remoto funcional com `host.docker.internal:9003`

---

## 🔒 Segurança

- Regras de segurança ativadas via `phpcs.xml` utilizando [pheromone/phpcs-security-audit](https://github.com/sektioneins/phpcs-security-audit)

---

## 👨‍💻 Desenvolvedor

Hamilton Gláucio de Oliveira Júnior  
📧 contato@hamiltonjunior.com.br  
📱 (87) 98115-3286  

---

## 📌 Observações

- Todas as ferramentas funcionam com `XDEBUG_MODE=off` para melhor performance
- O diretório `src/` está atualmente vazio — necessário adicionar código para cobertura e análise completa
- Todas as configurações estão centralizadas no diretório `.docker/php/`

---

## 🧪 Teste o Ambiente

Para validar rapidamente o setup, você pode criar um arquivo simples:

```php
// src/Sample.php
<?php
namespace App;
class Sample {
    public function ping(): string {
        return 'pong';
    }
}
```

E um teste correspondente em `tests/SampleTest.php`.

---
