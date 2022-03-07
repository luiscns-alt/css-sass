# Css - Sass

## Pré-processador CSS

Um pré-processador CSS é um programa que permite você gerar CSS a partir de uma sintaxe (en-US) única desse pré-processador. Existem muitos pré-processadores CSS para escolha, no entanto, a maioria deles irá adicionar algumas funcionalidades extras que não existem no CSS puro, como um mixin, seletores aninhados, herança de seletores, e assim por diante. Essas funcionalidades fazem a estrutura do CSS mais legível e fácil de manter.
Para usar um pré-processador, você deve instalar um compilador CSS no seu servidor web; Ou usar o pré-processador CSS para compilar no ambiente de desenvolvimento, e então fazer upload do arquivo CSS compilado para o servidor web.

## Sass

O Sass (Syntactically Awesome Style Sheets ou Folhas de Estilo Sintaticamente Impressionantes) é um dos pré-processadores mais utilizados em todo o mundo.

O Sass é considerado, por seus autores, uma extensão do CSS3, porque permite trabalhar com aninhamento de regras, variáveis, mixins, herança de seletores, etc.

## Configurando o Ambiente com Node.js

-   Primeiro, obtenha o [Node.js](https://nodejs.org/)
-   Crie um diretório chamado sass

```shell
  $ tree
    ├── dev
      └── my-styles.scss
    ├── dist
    │ └── my-styles.css
    ├── package.json
    └── gulpfile.js
```

-   Em dev criamos o arquivos SCSS.
-   Em dist será o local do CSS final
-   Em dist crie um arquivo chamado _my-styles.scss_ é adicionei o seguinte codigo:
    ```SCSS
    #my-div{
        color: red;
        &:hover{
            color: green;
        }
    }
    ```

### Instalando Gulp

O Gulp, que é um automatizador de tarefas. Faremos com que ele observe nosso diretório “dev” e, caso note alteração em algum arquivo, automaticamente irá compilar nossos arquivos para CSS.

No terminal execute o comando:

```shell
npm install gulp -g
```

Agora, abra o terminal no diretório “Sass” e execute o comando:

```shell
npm install gulp gulp-sass
```

Isso irá instalar em nosso projeto o Gulp e um plugin do Gulp para Sass.

Agora crie um arquivo chamado “gulpfile.js”. Nele criaremos uma função que irá automatizar a compilação do Sass.

No arquivo “gulpfile.js”, insira o seguinte código:

```js
var gulp = require('gulp'),
    sass = require('gulp-sass');

gulp.task('sass', function () {
    return gulp
        .src(['./dev/**/*.scss'])
        .pipe(
            sass({
                outputStyle: 'expanded',
                errLogToConsole: true,
            })
        )
        .pipe(gulp.dest('./dist'));
});

gulp.task('watch', function () {
    gulp.watch(['./dev/**/*.scss'], ['sass']);
});
```

Importamos as dependências e criamos duas tarefas.

A primeira irá pegar todos os arquivos “SCSS” em “/dev”, compilar e inserir em “/dist”.

A segunda irá observar todos os arquivos “SCSS” em “/dev”. Caso algum seja alterado, a tarefa “sass” será executada.

Para executar a compilação, basta executar o comando:

```shell
gulp sass
```

Para que a compilação seja feita automaticamente cada vez que algum arquivo for alterado, execute o comando:

```shell
gulp watch
```
